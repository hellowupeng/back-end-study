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

join()方法是一个同步方法。当线程终止时，会调用线程自身的notifyAll()方法，会通知所有等待在该线程对象上的线程。

