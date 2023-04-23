---
title: JAVA源码问题
date: 2020-05-14 13:54:19
tags: JAVA源码
categories: JAVA源码
---

## 概述

> 本章介绍JAVA源码问题

<!--more-->

## 正文

## 说说常见的集合有哪些吧？

答：Map 接口和 Collection 接口是所有集合框架的父接口：

1. Collection 接口的子接口包括：Set 接口和 List 接口；
2. Map 接口的实现类主要有：HashMap、TreeMap、Hashtable、ConcurrentHashMap 以及 Properties 等；
3. Set 接口的实现类主要有：HashSet、TreeSet、LinkedHashSet 等；
4. List 接口的实现类主要有：ArrayList、LinkedList、Stack 以及 Vector 等。

### 当两个对象的hashcode相同时会发生什么，如何获取对象？

因为hashcode相同，所以它们的bucket位置相同，‘碰撞’会发生。

两个对象的hashCode相同所以它们的bucket位置相同，找到bucket位置之后，会调用keys.equals()方法去找到链表中正确的节点 **`(key != null && key.equals(k)`**。

因为HashMap使用链表存储对象，这个Entry(包含有键值对的Map.Entry对象)会存储在链表中。这个时候要理解根据hashcode来划分的数组，如果数组的坐标相同，则进入链表这个数据结构中了，一般的添加都在最前面，也就是和数组下标直接相连的地方，链表长度到达8的时候，jdk1.8上升为红黑树。

### HashMap的大小超过了负载因子(load factor)定义的容量，怎么办

会调用**`resize()`**进行数组扩容。

## HashMap中的tableSizeFor方法

在使用指定数组的初始容量时上面说过，数组容量必须是2的次方。所以就需要通过算法将我们给定的数值转换成2的次方。

```java
// 这个方法可以将任意一个整数转换成2的次方。
static final int tableSizeFor(int cap) {
    int n = cap - 1;
    n |= n >>> 1;
    n |= n >>> 2;
    n |= n >>> 4;
    n |= n >>> 8;
    n |= n >>> 16;
    return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
}
```

## HashMap是线程安全的吗，为什么

HashMap底层是一个Entry数组，当发生hash冲突的时候，hashmap是采用链表的方式来解决的，在对应的数组位置存放链表的头结点。对链表而言，新加入的节点会从头结点加入。

1

```java
void addEntry(int hash, K key, V value, int bucketIndex) {
	Entry<K,V> e = table[bucketIndex];
        table[bucketIndex] = new Entry<K,V>(hash, key, value, e);
        if (size++ >= threshold)
            resize(2 * table.length);
    }
```

在hashmap做put操作的时候会调用到以上的方法。现在假如A线程和B线程同时对同一个数组位置调用addEntry，两个线程会同时得到现在的头结点，然后A写入新的头结点之后，B也写入新的头结点，那B的写入操作就会覆盖A的写入操作造成A的写入操作丢失

2

```java
final Entry<K,V> removeEntryForKey(Object key) {
        int hash = (key == null) ? 0 : hash(key.hashCode());
        int i = indexFor(hash, table.length);
        Entry<K,V> prev = table[i];
        Entry<K,V> e = prev;
 
        while (e != null) {
            Entry<K,V> next = e.next;
            Object k;
            if (e.hash == hash &&
                ((k = e.key) == key || (key != null && key.equals(k)))) {
                modCount++;
                size--;
                if (prev == e)
                    table[i] = next;
                else
                    prev.next = next;
                e.recordRemoval(this);
                return e;
            }
            prev = e;
            e = next;
        }
 
        return e;
    }
```

删除键值对的代码如上：

当多个线程同时操作同一个数组位置的时候，也都会先取得现在状态下该位置存储的头结点，然后各自去进行计算操作，之后再把结果写会到该数组位置去，其实写回的时候可能其他的线程已经就把这个位置给修改过了，就会覆盖其他线程的修改

3、addEntry中当加入新的键值对后键值对总数量超过门限值的时候会调用一个resize操作，代码如下：

```java
void resize(int newCapacity) {
        Entry[] oldTable = table;
        int oldCapacity = oldTable.length;
        if (oldCapacity == MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return;
        }
 
        Entry[] newTable = new Entry[newCapacity];
        transfer(newTable);
        table = newTable;
        threshold = (int)(newCapacity * loadFactor);
    }
```

这个操作会新生成一个新的容量的数组，然后对原数组的所有键值对重新进行计算和写入新的数组，之后指向新生成的数组。

当多个线程同时检测到总数量超过门限值的时候就会同时调用resize操作，各自生成新的数组并rehash后赋给该map底层的数组table，结果最终只有最后一个线程生成的新数组被赋给table变量，其他线程的均会丢失。而且当某些线程已经完成赋值而其他线程刚开始的时候，就会用已经被赋值的table作为原始数组，这样也会有问题。

## 哪些是线程安全的容器

同步容器类：

使用了synchronized
1.Vector
2.HashTable

并发容器：
3.ConcurrentHashMap:分段
4.CopyOnWriteArrayList：写时复制
5.CopyOnWriteArraySet：写时复制

### Hashtable和HashMap的区别

### HashMap多线程处理之快速失败机制

### jdk7和jdk8的HashMap实现的区别

### HashMap与LinkedHashMap和TreeMap的区别



