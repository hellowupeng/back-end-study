# LinkedList

🍎🍎

LinkedList<E>是一个泛型容器类，继承自AbstractSequentialList抽象类，实现了List<E>, Deque<E>, Cloneable, Serializable接口。

LinkedList类不是线程安全的。

## 基本用法

### 构造方法

```java
// 构造一个空列表
public LinkedList()
// 构造一个包含指定集合元素的列表
public LinkedList(Collection<? extends E> c)
```

## 实现原理

### 内部结构（主要）

LinkedList的内部实现是双向链表，每个元素在内存中都是单独存放的，元素之间通过链接连在一起（就像小朋友手拉手一样）。

为了表示这种链接关系，在内部定义了一个节点类（Node）：

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

Node表示节点，实例变量item指向实际的列表元素，next指向后一个节点，prev指向前一个节点。

LinkedList内部主要实例变量有size、first、last。

```java
transient int size = 0;
transient Node<E> first;
transient Node<E> last;
```

size表示链表长度，默认为0，first指向头节点，last指向尾节点，初始值都为null。