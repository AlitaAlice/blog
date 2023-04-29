---
title: HashMap相关
date: 2020-05-29 11:40:36
tags: JAVA集合
categories: JAVA集合
---

## 概述

> 本章介绍HashMap相关

<!--more-->

## 正文

## 1 基于拉链和线性探测法的散列表

https://alitaalice.online/2020/05/13/%E5%9F%BA%E4%BA%8E%E6%8B%89%E9%93%BE%E5%92%8C%E7%BA%BF%E6%80%A7%E6%8E%A2%E6%B5%8B%E6%B3%95%E7%9A%84%E6%95%A3%E5%88%97%E8%A1%A8/

## 2 hashcode()

https://alitaalice.online/2020/05/13/%E6%95%A3%E5%88%97%E8%A1%A8%E8%AF%A6%E8%A7%A3/

## 3 HashMap加载因子和初始容量

转载自https://www.cnblogs.com/aspirant/p/11470928.html4

### 4 当两个对象的hashcode相同时会发生什么，如何获取对象

因为hashcode相同，所以它们的bucket位置相同，‘碰撞’会发生。因为HashMap使用链表存储对象，这个Entry(包含有键值对的Map.Entry对象)会存储在链表中。这个时候要理解根据hashcode来划分的数组，如果数组的坐标相同，则进入链表这个数据结构中了，一般的添加都在最前面，也就是和数组下标直接相连的地方，链表长度到达8的时候，jdk1.8上升为红黑树.

### 5  HashMap中的tableSizeFor方法

在使用指定数组的初始容量时上面说过，**数组容量必须是2的次方。所以就需要通过算法将我们给定的数值转换成2的次方。**

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

### 6 重新调整HashMap大小存在什么问题吗

当重新调整HashMap大小的时候，确实存在条件竞争，因为如果两个线程都发现HashMap需要重新调整大小了，它们会同时试着调整大小。在调整大小的过程中，存储在链表中的元素的次序会反过来，因为移动到新的bucket位置的时候，HashMap并不会将元素放在链表的尾部，而是放在头部，这是为了避免尾部遍历(tail traversing)。如果条件竞争发生了，那么就死循环了。(多线程的环境下不使用HashMap）

HashMap的容量是有限的。当经过多次元素插入，使得HashMap达到一定饱和度时，Key映射位置发生冲突的几率会逐渐提高。这时候，HashMap需要扩展它的长度，也就是进行Resize。

1. 扩容：创建一个新的Entry空数组，长度是原数组的2倍。
2. ReHash：遍历原Entry数组，把所有的Entry重新Hash到新数组。

### 7 如果HashMap的大小超过了负载因子(load factor)定义的容量，怎么办？

默认的负载因子大小为0.75，也就是说，当一个map填满了75%的bucket时候，和其它集合类(如ArrayList等)一样，将会创建原来HashMap大小的两倍的bucket数组，来重新调整map的大小，并将原来的对象放入新的bucket数组中。这个过程叫作rehashing，因为它调用hash方法找到新的bucket位置。这个值只可能在两个地方，一个是原下标的位置，另一种是在下标为<原下标+原容量>的位置

### 8 我们可以使用自定义的对象作为HashMap的键吗

作为HashMap的key的自定义类需要重写hashCode()和equals()

```java
package cn.xxx.demo;
 
import java.util.HashMap;
import java.util.Map;
 
// 使用HashMap集合,存储自定义的对象。 如果自定义的对象作为键(键不能重复),需要重写自定义类型的hashCode()和equals()方法。
 
public class Demo {
	public static void main(String[] args) {
		function();
	}
 
	public static void function(){
		HashMap<Person, String> map = new HashMap<Person, String>();
		map.put(new Person("a",20), "里约热内卢");
		map.put(new Person("b",18), "索马里");
		map.put(new Person("b",18), "索马里");
		map.put(new Person("c",19), "百慕大");
		for(Person key : map.keySet()){  // 通过keySet()遍历
			String value = map.get(key);
			System.out.println(key+"..."+value);
		}
		System.out.println("===================");
		for(Map.Entry<Person, String> entry : map.entrySet()){  // 通过entrySet()遍历
			System.out.println(entry.getKey()+"..."+entry.getValue());
		}
	}
}
```

### 9 jdk7和jdk8的HashMap实现的区别

JDK7中的HashMap

基于链表+数组实现,底层维护一个Entry数组

```text
Entry<K,V>[] table;
```

根据计算的hashCode将对应的KV键值对存储到该table中，一旦发生hashCode冲突，那么就会将该KV键值对放到对应的已有元素的后面， 此时，形成了一个链表式的存储结构,如下图![](https://photos.alitaalice.cn/image/20200601154028.png)

JDK8中的HashMap

基于位桶+链表/红黑树的方式实现,底层维护一个Node数组

```text
Node<K,V>[] table;
```

在JDK7中HashMap,当成百上千个节点在hash时发生碰撞，存储一个链表中，那么如果要查找其中一个节点，那就不可避免的花费O(N)的查找时间，这将是多么大的性能损失,这个问题终于在JDK8中得到了解决。

JDK8中,HashMap采用的是位桶+链表/红黑树的方式,当链表的存储的数据个数大于等于8的时候，不再采用链表存储，而采用了红黑树存储结构。这是JDK7与JDK8中HashMap实现的最大区别。 如下图所示：![](https://photos.alitaalice.cn/image/20200601154120.png)

### 10  HashMap与LinkedHashMap和TreeMap Hashtable的区别

**HashMap**: 最常用的Map,它根据键的HashCode 值存储数据,根据键可以直接获取它的值，具有很快的访问速度。HashMap最多只允许一条记录的键为Null(多条会覆盖);允许多条记录的值为 Null。非同步的。 

**TreeMap**: 能够把它保存的记录根据键(key)排序,默认是按升序排序，也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。TreeMap不允许key的值为null。非同步的。 

**Hashtable:** 与 HashMap类似,不同的是:key和value的值均不允许为null;它支持线程的同步，即任一时刻只有一个线程能写Hashtable,因此也导致了Hashtable在写入时会比较慢。 

**LinkedHashMap**: 保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的.在遍历的时候会比HashMap慢。key和value均允许为空，非同步的。 

### 11 为什么 HashMap 中 String、Integer 这样的包装类适合作为 key 键，即为什么使用它们可以减少哈希碰撞？

答：因为 String、Integer 等包装类是 **final 类型的，具有不可变性，而且已经重写了 equals() 和 hashCode() 方法。**不可变性保证了计算 hashCode() 后键值的唯一性和缓存特性，不会出现放入和获取时哈希码不同的情况且读取哈希值的高效性，此外官方实现的 equals() 和 hashCode() 都是严格遵守相关规范的，不会出现错误

12.HashMap是线程安全的吗，为什么

13.哪些是线程安全的容器

同步容器类：

使用了synchronized
1.Vector
2.HashTable

并发容器：
3.ConcurrentHashMap:　底层哈希实现的同步Map(Set)。效率高，线程安全。使用系统底层技术实现线程安全。量级较synchronized低。key和value不能为null
4.CopyOnWriteArrayList：写时复制
5.CopyOnWriteArraySet：写时复制

