# ReadWriteLock实现原理

一旦任何一个线程获取了写锁，除了该线程自己，其它线程都将无法获取读锁和写锁。

ReentrantReadWriteLock实现了ReadWriteLock和Serializable接口。

##### ReentrantReadWriteLock结构（主要）

静态内部类ReadLock类型的变量readerLock

静态内部类WriteLock类型变量writerLock

Sync类型变量sync：Sync是一个继承AQS抽象类的抽象类，有两个实现类NonfairSync和FairSync，对应非公平锁和公平锁。