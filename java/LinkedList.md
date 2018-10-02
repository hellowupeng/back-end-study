# LinkedList

*复习（1）*

LinkedList是一个泛型容器类。

LinkedList类继承自AbstractSequentialList抽象类，实现了List<E>, Deque<E>, Cloneable, Serializable接口。

LinkedList类不是线程安全的。

## 基本用法

##### 构造方法

```java
public LinkedList()
public LinkedList(Collection<? extends E> c)
```

## 实现原理

##### 内部结构（主要）

LinkedList的内部实现是双向链表，每个元素在内存中都是单独存放的，元素之间通过链接连在一起，就像小朋友手拉手一样。

为了表示这种链接关系，在内部定义了一个节点类：

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

Node表示节点，item指向实际的元素，next指向后一个节点，prev指向前一个节点。

LinkedList内部实例变量：

```java
transient int size = 0;
transient Node<E> first;
transient Node<E> last;
```

size表示链表长度，默认为0，first指向头节点，last指向尾节点，初始值都为null。