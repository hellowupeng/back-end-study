# synchronized

复习（1）

## 一、synchronized

java关键字，可以用于修饰类的实例方法、静态方法和代码块。

synchronized实例方法保护的是当前实例对象this，this对象有一个锁和一个等待队列，锁只能被一个线程持有，其他试图获得同样锁的线程需要等待。

执行synchronized实例方法的过程大致是：

1）尝试获取锁，如果能够获得锁，继续下一步，否则加入等待队列，阻塞并等待唤醒。

2）执行实例方法体代码。

3）释放锁，如果等待队列上有等待的线程，从中取一个并唤醒，如果有多个等待的线程，唤醒哪一个是不一定的，不保证公平性。

线程不能获得锁时，会加入等待队列等待，线程状态会变为BLOCKED。

对静态方法，保护的是类对象。synchronized静态方法和synchronized实例方法保护的是不同的对象，不同的两个线程。

synchronized是一种互斥锁。一次只允许一个线程访问同步代码。

可重入性、内存可见性。

## 二、synchronized实现原理

java中每一个对象都可以作为锁，这是synchronized实现同步的基础：

1 普通同步方法，锁是当前实例对象

2 静态同步方法，锁是当前类的class对象

3 同步方法块，锁是括号里面的对象

##### 同步代码块

使用monitorenter和monitorexit指令实现。

对于synchronized语句当java源代码被javac编译成字节码（bytecode）时，会在同步块的入口位置和退出位置分别插入monitorenter和monitorexit字节码指令。JVM需要保证每一个monitorenter都有一个monitorexit与之相对应。任何对象都有一个monitor与之相关联，当且一个monitor被持有之后，它将处于锁定状态。线程执行到monitorenter指令时，将会尝试获取对象所对应的monitor所有权，即尝试获取对象的锁。

（简单来说在JVM中monitorenter和monitorexit字节码依赖于底层的操作系统的Mutex Lock来实现的）

##### 同步方法

synchronized方法则会被编译成普通的方法调用和返回指令，如：invokevirtual、areturn指令，在VM字节码层面并没有任何特别的指令来实现被synchronized修饰的方法，而是在Class文件的方法表中将该方法的access_flags字段中的synchronized标志位置1，表示该方法是同步方法并使用调用该方法的对象或该方法所属的Class在JVM的内部对象表示Klass作为锁对象。



##### 参考

1 [JVM内部细节之一：synchronized关键字及实现细节（轻量级锁Lightweight Locking）](https://www.cnblogs.com/javaminer/p/3889023.html)
