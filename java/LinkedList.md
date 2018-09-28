# LinkedList

LinkedList是一个泛型容器类。

LinkedList类继承自AbstractSequentialList抽象类，实现了List<E>, Deque<E>, Cloneable, Serializable接口。

LinkedList类不是线程安全的。

## 基本用法

##### 构造方法

构造一个空列表：

```java
public LinkedList()
```

使用指定集合构造一个列表：

```java
public LinkedList(Collection<? extends E> c)
```

## 实现原理

##### 内部结构（主要）

LinkedList的内部实现是双向链表，每个元素在内存中都是单独存放的，元素之间通过链接连在一起，就像小朋友手拉手一样。

为了表示

```java
private static class Node<E> {
    E item;
    Node<E> next;
    Node<E> prev;
    Node(Node<E> prev, E element, Node<E> next) {
        this.item = element;
        this.next = next;
        this.prev = prev;
    }
}
```