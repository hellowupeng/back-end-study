# 线程（Thread）的状态

Thread有6种状态:

```java
public enum State {
    New,
    RUNNABLE,
    BLOCKED,
    WAITING,
    TIMED_WAITING,
    TERMINATED;
}
```

1）（NEW）没有调用start的线程状态为NEW。

2）（TERMINATED）线程运行结束后状态为TERMINATED。

3）（RUNNABLE）调用start后线程在执行run方法且没有阻塞状态为RUNNABLE，不过RUNNABLE不代表CPU一定在执行该线程的代码，可能正在执行也可能在等待操作系统分配时间片，只是他没有在等待其他条件。

4）（BLOCKED）线程在等待获取monitor锁进入同步（synchronized）块或方法的状态为BLOCKED。

5）（WAITING）在调用了`Object.wait()`和`Thread.join()`方法且都未指定timeout，以及调用了`LockSupport.park()`方法后Thread会处于WAITING状态。

（调用了`Object.wait()`方法的线程在等待另一个线程调用`Object.notify()`或`Object.notifyAll()`。调用了`Thread.join()`方法的线程在等待指定线程终止。）

6）（TIMED_WAITING）在调用了`Thread.sleep()` `Object.wait()` `thread.join()` `LockSupport.parkNanos()` `LockSupport.parkUntil()`方法并指定了等待时间的线程会处于TIMED_WAITING状态。

