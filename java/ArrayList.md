# ArrayList

🍎

ArrayList是一个动态数组容器类，也是一个泛型容器。

ArrayList类继承自AbstractList类， 实现了List<E>, RandomAccess, Cloneable, Serializable接口。

## 基本用法

##### 构造函数

使用指定的初始capacity构造一个空列表：

```java
public ArrayList(int initialCapacity);
```

构造一个初始capacity为0的空列表：

```java
public ArrayList();
```

构造一个包含指定元素集合的列表：

```java
public ArrayList(Collection<? extends E> c);
```

##### 

## 实现原理

##### 内部结构（主要）

```java
transient Object[] elementData;
private int size;
```

内部有一个数组elementData，一般会有一些预留的空间，有一个整数size记录实际的元素个数（java 8）。

各种public方法内部操作的基本都是这个数组和这个整数，elementData会随着实际元素个数的增多而重新分配，size则始终记录实际的元素个数。

##### 添加元素

列表添加元素：

```java
public boolean add(E e) {
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    elementData[size++] = e;
    return true;
}
```

ensureCapacityInternal方法确保数组的容量是足够的，否则调用calculateCapacity计算新的capacity，并调用grow方法根据capacity创建一个新数组并复制原数组内容到新数组。

##### 移除元素

列表移除元素：

```java
public E remove(int index) {
    rangeCheck(index);

    modCount++;
    E oldValue = elementData(index);

    int numMoved = size - index - 1;
    if (numMoved > 0)
        System.arraycopy(elementData, index+1, elementData, index,
                         numMoved);
    elementData[--size] = null; // clear to let GC do its work

    return oldValue;
}
```

计算要移动的个数，从index往后的元素都往前移动一位，实际使用System.arraycopy方法移动元素。更新size，同时将最后一个位置设为null。
