# Q1

## java

## 数据库、缓存

## 框架

## 网络

## 算法、数据结构

## 一

1. [常用的异常类型?](https://github.com/hellowupeng/interview/blob/master/java/常用的异常类型.md)
2. [session](https://github.com/hellowupeng/interview/blob/master/java/session.md)
3. [java锁](https://github.com/hellowupeng/interview/blob/master/java/java锁.md)
4. [Synchronized实现原理](https://github.com/hellowupeng/interview/blob/master/java/Synchronized实现原理.md)
5. [ReentrantLock实现原理](https://github.com/hellowupeng/interview/blob/master/java/ReentrantLock实现原理.md)
6. [ReadWriteLock实现原理](https://github.com/hellowupeng/interview/blob/master/java/ReadWriteLock实现原理.md)
7. [gc原理](https://github.com/hellowupeng/interview/blob/master/java/gc原理.md)
8. hashmap
9. [ArrayList](https://github.com/hellowupeng/interview/blob/master/java/ArrayList.md)
10. [LinkedList](https://github.com/hellowupeng/interview/blob/master/java/LinkedList.md)
11. LinkedList, ArrayList 区别
12. [Spring AOP实现原理](https://github.com/hellowupeng/interview/blob/master/framework/aop%20原理.md)
13. 多线程
14. kafka 原理和容错
15. spark hadoop 原理
16. redis 同步机制
17. [ClassLoader 机制](https://github.com/hellowupeng/interview/blob/master/java/ClassLoader%20机制.md)
18. Http 协议
19. cookie的限制
20. 如何设计一个分步式登录系统？
21. Spring的加载过程
22. 自己有没有写过类似Spring这样的AOP事务？
23. atomic 与 volatile的区别？
24. Thread的 notify()给notifyAll()的区别?
25. notifiy()是唤醒的那一个线程?
26. Thread.sleep()唤醒以后是否需要重新竞争？
27. 单例有多少种写法? 有什么区别? 你常用哪一种单例，为什么用这种？
28. 问一个Thread.join()相关的问题?
29. 写一个JAVA死锁的例子?
30. 如何解决死锁?
31. GC回收算法,及实现原理?
32. HashMap数据存储结构? key重复了怎么办? 是如何解决的?
33. Spring AOP的实现原理，底层用什么实现的？

## 二

重点是面试技术原理，以及对技术的热情和专研程度：

1. Java的高级知识
2. 开源框架的原理
3. JVM
4. 多线程
5. 高并发
6. 中间件
7. 之前项目经历，运用的技术，遇到的问题，如何解决，个人有什么收获和成长；
8. 对于技术的热情（平时是否看些技术书籍，逛论坛，写博客，写源代码或程序等）；

## java

1. 我们主要考核的是网络nio 分布式数据库高并发大数据
2. 自定义表格的实现?
3. 动态表单设计?
4. in-jvm（必考）以及jmm缓存模型如何调优?
5. 常用的RPC框架
6. nio和io
7. 并发编程，设计模式
8. 地图组件?
9. hashmap有什么漏洞会导致他变慢？
10. 如何给hashmap的key对象设计他的hashcode？
11. 泛型通配符?在什么情况下使用？
12. 后端方面：redis?分布式框架dubbo(阿里巴巴开源框架)?设计模式?
13. 场景式的问题:秒杀,能列出常见的排队、验证码、库存扣减方式对系统高并发的影响?
14. 能根据实际的需要构建缓存结构提高提高网站的访问速度，熟练使用ehcache、oscache，了解memcache。
15. 了解基于dns轮询的负载均衡，熟练配置web服务器实现负载均衡，程序级能综合使用基于hash或取模等手段实现软负载。
16. 熟悉分布式数据库设计和优化技术，熟练使用mysql、oracle、SqlServer等主流数据库，熟悉hadoop hbase mangodb redis ehcache、oscache memcache。对于大数据量的数据库处理采用分表分库、数据库读写分离、建立缓存等手段优化性能。
17. 熟练掌握lucene，能基于lucene开发大型的搜索引擎，并能用lucene来改善和优化数据库的like查询。

## 四

1. 缓存的使用，如果现在需要实现一个简单的缓存，供搜索框中的ajax异步请求调用，使用什么结构？
2. 内存中的缓存不能一直存在，用什么算法定期将搜索权重较低的entry去掉？
3. TCP如何保证安全性
4. 红黑树的问题，B+数
5. JDK1.8中对HashMap的增强，如果一个桶上的节点数量过多，链表+数组的结构就会转换为红黑树。
6. 项目中使用的单机服务器，如果将它部署成分布式服务器？
7. MySQL的常见优化方式、定为慢查询
8. 手写一个线程安全的单例模式

## 五

1. 算法和数据结构数组、链表、二叉树、队列、栈的各种操作（性能，场景）
2. 二分查找和各种变种的二分查找
3. 各类排序算法以及复杂度分析（快排、归并、堆）
4. 各类算法题（手写）
5. 理解并可以分析时间和空间复杂度。
6. 动态规划（笔试回回有。。）、贪心。
7. 红黑树、AVL树、Hash树、Tire树、B树、B+树。
8. 图算法（比较少，也就两个最短路径算法理解吧）
9. 计算机网络OSI7层模型（TCP4层）每层的协议
10. get/post 以及幂等性
11. http 协议头相关
12. 网络攻击（CSRF、XSS）
13. [TCP/IP三次握手、四次挥手](https://github.com/hellowupeng/interview/blob/master/network/TCPIP三次握手、四次挥手.md)
14. TCP与UDP比较
15. DDos攻击
16. (B)IO/NIO/AIO三者原理，各个语言是怎么实现的
17. Netty
18. Linux内核select poll epoll
19. 数据库（最多的还是mysql，Nosql有redis）索引（包括分类及优化方式，失效条件，底层结构）
20. sql语法（join，union，子查询，having，group by）
21. [引擎对比（InnoDB，MyISAM）](https://github.com/hellowupeng/interview/blob/master/db/MySQL引擎对比（InnoDB，MyISAM）.md)
22. 数据库的锁（行锁，表锁，页级锁，意向锁，读锁，写锁，悲观锁，乐观锁，以及加锁的select sql方式）
23. 隔离级别，依次解决的问题（脏读、不可重复读、幻读）
24. [事务的ACID](https://github.com/hellowupeng/interview/blob/master/db/事务的ACID.md)
25. B树、B+树
26. 优化（explain，慢查询，show profile）
27. 数据库的范式
28. 分库分表，主从复制，读写分离。
29. Nosql相关（redis和memcached区别之类的，如果你熟悉redis，redis还有一堆要问的）
30. 操作系统：进程通信IPC（几种方式），与线程区别
31. OS的几种策略（页面置换，进程调度等，每个里面有几种算法）
32. 互斥与死锁相关的
33. linux常用命令（问的时候都会给具体某一个场景）
34. Linux内核相关（select、poll、epoll）
35. 编程语言（这里只说Java）：把我之后的面经过一遍，Java感觉覆盖的就差不多了，不过下面还是分个类。
36. Java基础（面向对象、四个特性、重载重写、static和final等等很多东西）
37. 集合（HashMap、ConcurrentHashMap、各种List，最好结合源码看）
38. 并发和多线程（线程池、SYNC和Lock锁机制、线程通信、volatile、ThreadLocal、CyclicBarrier、Atom包、CountDownLatch、AQS、CAS原理等等）
39. JVM（内存模型、GC垃圾回收，包括分代，GC算法，收集器、类加载和双亲委派、JVM调优，内存泄漏和内存溢出）
40. IO/NIO相关
41. 反射和代理、异常、Java8相关、序列化
42. 设计模式（常用的，jdk中有的）
43. Web相关（servlet、cookie/session、Spring)

## 六

1. 内存模型
2. 类加载机制
3. GC
4. JVM调优
5. 线程池原理
6. 动态代理
7. 悲观锁乐观锁
8. 高并发问题
9. 事务隔离级别
10. 索引原理
11. 限流
12. 分库分表
13. 分布式事务提交
14. 微服务
15. dubbo原理

## 七

1. java锁优化
2. Synchronized源码分析
3. ReentrantLock源码分析
4. ReadWriteLock源码分析
5. AbstractQueuedSynchronizer源码分析
6. 自旋锁
7. InnoDB深入

###### 参考：

1.[史上最全阿里技术面试题目](https://www.toutiao.com/a6581717700844716552/?tt_from=weixin&utm_campaign=client_share&wxshare_count=1&timestamp=1537788762&app=news_article&utm_source=weixin&iid=44091158662&utm_medium=toutiao_ios&group_id=6581717700844716552)