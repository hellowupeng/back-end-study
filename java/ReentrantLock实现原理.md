# ReentrantLock实现原理

*复习（1）*

##### 可重入锁

ReentrantLock是可重入锁，可重入锁就是当前持有该锁的线程能够多次获取该锁，无须等待。

可重入锁是通过记录锁的持有线程和持有数量来实现的。比如，当调用被synchronized保护的代码时，检查对象是否已被锁，如果是，再检查是否是被当前线程锁定，如果是，增加持有数量，如果不是被当前线程锁定，才加入等待队列，当释放锁时，减少持有数量，当数量变为0时才释放整个锁。

可重入锁的实现要从ReentrantLock的一个内部类Sync的父类说起，Sync的父类是AbstractQueuedSynchronizer（AQS）

##### AQS

AQS是JDK1.5提供的一个基于FIFO等待队列实现的一个用于实现同步器的基础框架。AQS的核心思想是基于volatile int state这样的一个属性同时配合Unsafe工具对其原子性的操作来实现对当前锁的状态进行修改。当state的值为0的时候，标识该Lock不被任何线程所占有。

**ReentrantLock锁的结构**

ReentrantLock主要包括一个内部抽象类Sync以及Sync抽象类的两个实现类FairSync、NonfairSync，分别实现公平锁和非公平锁。

**AQS的等待队列**

AQS的等待队列是基于一个双向链表实现的，head节点不关联线程，线程会按照先后顺序被串联到这个队列上。末尾的线程会被当做队列的tail。

1）入队列
```java
public final void acquire(int arg) {
    if (!tryAcquire(arg) &&
        acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
        selfInterrupt();
}
```
三个线程同时进来，他们会首先会通过CAS去修改state的状态，如果修改成功，那么竞争成功，因此这个时候三个线程只有一个CAS成功，其他两个线程失败，也就是tryAcquire返回false。

接下来，addWaiter会把将当前线程关联的EXCLUSIVE类型的节点入队列：
```java
private Node addWaiter(Node mode) {
    Node node = new Node(Thread.currentThread(), mode);
    Node pred = tail;
    if (pred != null) {
        node.prev = pred;
        if (compareAndSetTail(pred, node)) {
            pred.next = node;
            return node;
        }
    }
    enq(node);
    return node;
}
```
如果队尾节点不为null，则说明队列中已经有线程在等待了，那么直接入队尾。对于我们举的例子，这边的逻辑应该是走enq，也就是开始队尾是null，其实这个时候整个队列都是null的。
```java
private Node enq(final Node node) {
    for (;;) {
        Node t = tail;
        if (t == null) { // Must initialize
            if (compareAndSetHead(new Node()))
                tail = head;
        } else {
            node.prev = t;
            if (compareAndSetTail(t, node)) {
                t.next = node;
                return t;
            }
        }
    }
}
```
如果Thread2和Thread3同时进入了enq，同时t==null，则进行CAS操作对队列进行初始化，这个时候只有一个线程能够成功，然后他们继续进入循环，第二次都进入了else代码块，这个时候又要进行CAS操作，将自己放在队尾，因此这个时候又是只有一个线程成功，我们假设是Thread2成功，哈哈，Thread2开心的返回了，Thread3失落的再进行下一次的循环，最终入队列成功，返回自己。

2）并发问题

多个线程都通过【CAS+死循环】这个free-lock黄金搭档来对队列进行修改，每次能够保证只有一个成功，如果失败下次重试，如果是N个线程，那么每个线程最多loop N次，最终都能够成功。

3）挂起等待线程

上面只是addWaiter的实现部分，那么节点入队列之后会继续发生什么呢？那就要看看acquireQueued是怎么实现的。

1 对于Thread2来说，它的prev指向HEAD，因此会首先再尝试获取锁一次，如果失败，则会将HEAD的waitStatus值为SIGNAL，下次循环的时候再去尝试获取锁，如果还是失败，且这个时候prev节点的waitStatus已经是SIGNAL，则这个时候线程会被通过LockSupport挂起

2 对于Thread3来说，它的prev指向Thread2，因此直接看看Thread2对应的节点的waitStatus是否为SIGNAL，如果不是则将它设置为SIGNAL，再给自己一次去看看自己有没有资格获取锁，如果Thread2还是挡在前面，且它的waitStatus是SIGNAL，则将自己挂起。

如果Thread1死死的握住锁不放，那么Thread2和Thread3现在的状态就是挂起状态啦，而且HEAD，以及Thread的waitStatus都是SIGNAL，尽管他们在整个过程中曾经数次去尝试获取锁，但是都失败了，失败了不能死循环呀，所以就被挂起了

**锁释放-等待线程唤起**

我们来看看当Thread1这个时候终于做完了事情，调用了unlock准备释放锁，这个时候发生了什么。
```java
public final boolean release(int arg) {
    if (tryRelease(arg)) {
        Node h = head;
        if (h != null && h.waitStatus != 0)
            unparkSuccessor(h);
        return true;
    }
    return false;
}
```
首先，Thread1会修改AQS的state状态，加入之前是1，则变为0，注意这个时候对于非公平锁来说是个很好的插入机会，举个例子，如果锁是公平锁，这个时候来了Thread4，那么这个锁将会被Thread4抢去。。。

我们继续走常规路线来分析，当Thread1修改完状态了，判断队列是否为null，以及队头的waitStatus是否为0，如果waitStatus为0，说明队列无等待线程，按照我们的例子来说，队头的waitStatus为SIGNAL=-1，因此这个时候要通知队列的等待线程，可以来拿锁啦，这也是unparkSuccessor做的事情，unparkSuccessor主要做三件事情：

1 将队列头的waitstatus设置为0

2 通过从队列尾部向队列头部移动，找到最后一个waitstatus<=0的那个节点，也就是离队头最近的没有被cancelled的那个节点，队头这时候指向这个节点。

3 将这个节点唤醒。

每次唤醒仅仅唤醒队头等待线程，让队头等待线程先出。

##### 参考

1 [扒一扒ReentrantLock以及AQS实现原理](https://my.oschina.net/andylucc/blog/651982)
