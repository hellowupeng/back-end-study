## 同步屏障CyclicBarrier？

CyclicBarrier的字面意思是可循环使用（Cyclic）的屏障（Barrier）。它要做的事情是，让一组线程到达一个屏障（也可以叫同步点）时被阻塞，直到最后一个线程到达屏障时，屏障才会开门，所有被屏障拦截的线程才会继续执行。

CyclicBarrier默认的构造方法是CyclicBarrier(int parties)，其参数表示屏障拦截的线程数量，每个线程调用await方法告诉CyclicBarrier我已经到达了屏障，然后当前线程被阻塞。

CyclicBarrier还提供了一个更高级的构造函数CyclicBarrier(int parties, Runnable barrier-Action)，用于在线程到达屏障时，优先执行barrierAction，方便处理更复杂的业务场景。

（应用场景）CyclicBarrier可以用于多线程计算数据，最后合并计算结果的场景。

（实现）内部阻塞控制主要由一个重入锁（ReentrantLock）和Condition实现。

##### CyclicBarrier与CountDownLatch的区别

CountDownLatch的计数器只能使用一次，而CyclicBarrier的计数器可以使用reset()方法重置。所以CyclicBarrier能处理更为复杂的业务场景。例如，如果计算发生错误，可以重置计数器，并让线程重新执行一次。