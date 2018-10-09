# Thread.join()

*复习（1）*

如果一个线程A执行了thread.join()语句，其含义是：当前线程A等待thread线程终止后才从thread.join()返回。

```Java
// 加锁当前线程对象
public final synchronized void join() throws InterruptedException {
    // 条件不满足，继续等待
    while (isAlive()) {
        wait(0);
    }
    // 条件符合，方法返回
}
```

join()方法是一个同步方法。join用于让当前执行线程等待join线程执行结束。其实现原理是不停检查join线程是否存活，如果join线程存活则让当前线程永远等待。当join线程终止时，会调用线程自身的notifyAll()方法，会通知所有等待在该线程对象上的线程。调用notifyAll()方法是在JVM里实现的，所以在JDK里看不到。

