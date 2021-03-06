# ReentrantReadWriteLock实现原理？

ReentrantReadWriteLock的实现主要包括：读写状态的设计、写锁的获取与释放、读锁的获取与释放以及锁降级。

### 1.读写状态的设计

读写锁依赖自定义队列同步器来实现同步功能，而读写状态就是其同步器的同步状态。读写锁的自定义队列同步器在同步状态（一个整型变量）上维护多个读线程和一个写线程的状态。

（如果在一个整型变量上维护多种状态，就一定需要“按位切割使用”这个变量）读写锁将变量切分成了两个部分，高16位表示读，低16位表示写。读写锁通过位运算确定读和写各自的状态。假设当前同步状态值为S，写状态等于S&0x0000FFFF（将高16位全部抹去），读状态等于S>>>16（无符号补0右移16位）。当写状态增加1时，等于S+1，当读状态增加1时，等于S+(1<<16)，也就是S+0x00010000。

### 2.写锁的获取与释放

写锁是一个支持重进入的排它锁。如果当前线程已经获取了写锁，则增加写状态。如果当前线程在获取写锁时，读锁已经被获取（读状态不为0）或者该线程不是已经获取写锁的线程，则当前线程进入等待状态。

写锁的释放与ReentrantLock的释放过程类似，每次释放均减少写状态，当写状态为0时表示写锁已被释放，从而等待的读写线程能够继续访问读写锁，同时上一次写线程的修改对后续读线程可见。

### 3.读锁的获取与释放

读锁是一个支持重进入的共享锁，它能够被多个线程同时获取，在没有其他写线程访问（或者写状态为0）时，读锁总会被成功获取，而所做的也只是（线程安全的）增加读状态。如果当前线程已经获取了读锁，则增加读状态。如果当前线程在获取读锁时，写锁已被其他线程获取，则进入等待状态。

读锁的每次释放（线程安全的，可能有多个读线程同时释放读锁）均减少读状态，减少的值是（1<<16）。

### 4.锁降级

锁降级指的是写锁降级称为读锁。锁降级是指把持住（当前拥有的）写锁，再获取到读锁，随后释放（先前拥有的）写锁的过程。