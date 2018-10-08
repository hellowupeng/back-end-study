# Q1

## java

1. [常用的异常类型?](https://github.com/hellowupeng/interview/blob/master/java/常用的异常类型.md)
2. hashmap原理
3. [ArrayList](https://github.com/hellowupeng/interview/blob/master/java/ArrayList.md)
4. [LinkedList](https://github.com/hellowupeng/interview/blob/master/java/LinkedList.md)
5. LinkedList, ArrayList 区别
6. [ClassLoader 机制](https://github.com/hellowupeng/interview/blob/master/java/ClassLoader%20机制.md)
7. HashMap数据存储结构? key重复了怎么办? 是如何解决的?
8. hashmap有什么漏洞会导致他变慢？
9. 如何给hashmap的key对象设计他的hashcode？
10. 泛型通配符?在什么情况下使用？
11. JDK1.8中对HashMap的增强，如果一个桶上的节点数量过多，链表+数组的结构就会转换为红黑树。
12. ConcurrentHashMap
13. 各种List
14. 面向对象
15. 四个特性
16. 重载重写
17. static和final等
18. 反射和代理
19. Java8相关
20. 序列化
21. 类加载机制
22. 动态代理

## Java并发编程

1. [Synchronized](https://github.com/hellowupeng/interview/blob/master/java/Synchronized实现原理.md)
2. [java锁](https://github.com/hellowupeng/interview/blob/master/java/java锁.md)
3. [ReentrantLock实现原理](https://github.com/hellowupeng/interview/blob/master/java/ReentrantLock实现原理.md)
4. [ReadWriteLock实现原理](https://github.com/hellowupeng/interview/blob/master/java/ReadWriteLock实现原理.md)
5. atomic 与 volatile的区别？
6. [Thread的notify()和notifyAll()的区别?](https://github.com/hellowupeng/interview/blob/master/java/Thread的notify()和notifyAll()的区别.md)
7. [notifiy()是唤醒的哪一个线程?](https://github.com/hellowupeng/interview/blob/master/java/notifiy()是唤醒的那一个线程.md)
8. [Thread.sleep()唤醒以后是否需要重新竞争？](https://github.com/hellowupeng/interview/blob/master/java/Thread.sleep()唤醒以后是否需要重新竞争？.md)
9. [Thread.join()](https://github.com/hellowupeng/interview/blob/master/java/Thread.join().md)
10. 写一个JAVA死锁的例子?
11. 如何解决死锁?
12. [手写一个线程安全的单例模式](https://github.com/hellowupeng/interview/blob/master/java/手写一个线程安全的单例模式.md)
13. 互斥与死锁相关的
14. [线程池](https://github.com/hellowupeng/interview/blob/master/java/线程池.md)
15. SYNC和Lock锁机制
16. 线程通信
17. [volatile](https://github.com/hellowupeng/interview/blob/master/java/volatile.md)
18. [ThreadLocal](https://github.com/hellowupeng/interview/blob/master/java/ThreadLocal.md)
19. CyclicBarrier
20. Atom包
21. CountDownLatch
22. AQS
23. CAS原理
24. IO/NIO相关
25. 悲观锁乐观锁

##### 其他

1. [等待/通知机制](https://github.com/hellowupeng/interview/blob/master/java/等待通知机制.md)
2. [线程（Thread）的状态](https://github.com/hellowupeng/interview/blob/master/java/线程（Thread）的状态.md)

## JVM

1. [gc原理](https://github.com/hellowupeng/interview/blob/master/java/gc原理.md)
2. GC回收算法,及实现原理?
3. in-jvm（必考）以及jmm缓存模型如何调优?
4. JVM（内存模型、GC垃圾回收，包括分代，GC算法，收集器、类加载和双亲委派、JVM调优，内存泄漏和内存溢出）
5. 内存模型
6. GC
7. JVM调优

## 数据库、缓存

1. redis 同步机制
2. 能根据实际的需要构建缓存结构提高网站的访问速度，熟练使用ehcache、oscache，了解memcache。
3. 熟悉分布式数据库设计和优化技术，熟练使用mysql、oracle、SqlServer等主流数据库，熟悉hadoop hbase mangodb redis ehcache、oscache memcache。对于大数据量的数据库处理采用分表分库、数据库读写分离、建立缓存等手段优化性能。
4. 缓存的使用，如果现在需要实现一个简单的缓存，供搜索框中的ajax异步请求调用，使用什么结构？
5. 内存中的缓存不能一直存在，用什么算法定期将搜索权重较低的entry去掉？
6. MySQL的常见优化方式、定为慢查询
7. 数据库（最多的还是mysql，Nosql有redis）索引（包括分类及优化方式，失效条件，底层结构）
8. sql语法（join，union，子查询，having，group by）
9. [引擎对比（InnoDB，MyISAM）](https://github.com/hellowupeng/interview/blob/master/db/MySQL引擎对比（InnoDB，MyISAM）.md)
10. 数据库的锁（行锁，表锁，页级锁，意向锁，读锁，写锁，悲观锁，乐观锁，以及加锁的select sql方式）
11. 隔离级别，依次解决的问题（脏读、不可重复读、幻读）
12. [事务的ACID](https://github.com/hellowupeng/interview/blob/master/db/事务的ACID.md)
13. 优化（explain，慢查询，show profile）
14. 数据库的范式
15. 分库分表，主从复制，读写分离。
16. Nosql相关（redis和memcached区别之类的，如果你熟悉redis，redis还有一堆要问的）
17. 分布式数据库
18. 事务隔离级别
19. 索引原理
20. 分库分表
21. 分布式事务提交

## 框架

1. [Spring AOP实现原理](https://github.com/hellowupeng/interview/blob/master/framework/aop%20原理.md)
2. kafka 原理和容错
3. spark hadoop 原理
4. Spring的加载过程
5. Spring AOP的实现原理，底层用什么实现的？
6. 自己有没有写过类似Spring这样的AOP事务？
7. 常用的RPC框架
8. nio和io
9. 分布式框架dubbo(阿里巴巴开源框架)
10. 熟练掌握lucene，能基于lucene开发大型的搜索引擎，并能用lucene来改善和优化数据库的like查询。
11. Netty
12. (B)IO/NIO/AIO三者原理，各个语言是怎么实现的
13. Web相关（servlet、cookie/session、Spring)
14. dubbo原理

## 网络

1. Http 协议
2. TCP如何保证安全性
3. 计算机网络OSI7层模型（TCP4层）每层的协议
4. get/post 以及幂等性
5. http 协议头相关
6. 网络攻击（CSRF、XSS）
7. [TCP/IP三次握手、四次挥手](https://github.com/hellowupeng/interview/blob/master/network/TCPIP三次握手、四次挥手.md)
8. TCP与UDP比较
9. DDos攻击

## 算法、数据结构

1. 红黑树的问题，B+树
2. 算法和数据结构数组、链表、二叉树、队列、栈的各种操作（性能，场景）
3. 二分查找和各种变种的二分查找
4. 各类排序算法以及复杂度分析（快排、归并、堆）
5. 各类算法题（手写）
6. 理解并可以分析时间和空间复杂度。
7. 动态规划（笔试回回有。。）、贪心。
8. 红黑树、AVL树、Hash树、Tire树、B树、B+树。
9. 图算法（比较少，也就两个最短路径算法理解吧）
10. B树、B+树

## 设计模式

1. 单例有多少种写法? 有什么区别? 你常用哪一种单例，为什么用这种？
2. 设计模式（常用的，jdk中有的）

## 服务器

1. 项目中使用的单机服务器，如果将它部署成分布式服务器？
2. 了解基于dns轮询的负载均衡，熟练配置web服务器实现负载均衡，程序级能综合使用基于hash或取模等手段实现软负载。
3. 限流

## Linux

1. Linux内核select poll epoll
2. linux常用命令（问的时候都会给具体某一个场景）
3. Linux内核相关（select、poll、epoll）

## 操作系统

1. 操作系统：进程通信IPC（几种方式），与线程区别
2. OS的几种策略（页面置换，进程调度等，每个里面有几种算法）

## 系统设计

1. 如何设计一个分步式登录系统？
2. cookie的限制
3. [session](https://github.com/hellowupeng/interview/blob/master/java/session.md)
4. 自定义表格的实现?
5. 动态表单设计?
6. 地图组件?
7. 场景式的问题:秒杀,能列出常见的排队、验证码、库存扣减方式对系统高并发的影响?

## 项目

1. 之前项目经历，运用的技术，遇到的问题，如何解决，个人有什么收获和成长；
2. 对于技术的热情（平时是否看些技术书籍，逛论坛，写博客，写源代码或程序等）；

## 架构

1. 微服务
2. 高并发问题

## 其他

1. Synchronized源码分析
2. ReentrantLock源码分析
3. ReadWriteLock源码分析
4. AbstractQueuedSynchronizer源码分析
5. 自旋锁
6. InnoDB深入

###### 参考：

1.[史上最全阿里技术面试题目](https://www.toutiao.com/a6581717700844716552/?tt_from=weixin&utm_campaign=client_share&wxshare_count=1&timestamp=1537788762&app=news_article&utm_source=weixin&iid=44091158662&utm_medium=toutiao_ios&group_id=6581717700844716552)