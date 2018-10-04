# ThreadLocal

*复习（1）*

ThreadLocal，线程变量，是一个以ThreadLocal对象为键、任意对象为值的存储结构。这个结构被附带在线程上，也就是说一个线程可以根据一个ThreadLocal对象查询到绑定在这个线程上的一个值。

##### 参考资料

1. 《Java并发编程的艺术》4.3.6 ThreadLocal的使用