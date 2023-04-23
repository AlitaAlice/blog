---
title: ConcurrentHashMap
date: 2020-09-09 11:39:36
tags: JUC
categories: JUC
---

## 概述

> 本章介绍ConcurrentHashMap

<!--more-->

## 正文

ConcurrentHashMap是线程安全且高效的HashMap。在介绍Concurrenthashmap之前，我们先来看一下HashMap。

**1.  HashMap概述**

​    HashMap是基于哈希表的Map接口的非同步实现。此实现提供所有可选的映射操作，并允许使用null值和null键（除了不同步和允许使用 null 之外，HashMap 类与 Hashtable 大致相同）。此类不保证映射的顺序，特别是它不保证该顺序恒久不变。

　　值得注意的是HashMap不是线程安全的，如果想要线程安全的HashMap，可以通过Collections类的静态方法synchronizedMap获得线程安全的HashMap。



```
 Map map = Collections.synchronizedMap(new HashMap());
```

## ** **

## **2、HashMap的数据结构**



HashMap的底层主要是基于***\*数组和链表\****来实现的，它之所以有相当快的查询速度主要是因为它是通过计算散列码来决定存储的位置。HashMap中主要是通过key的hashCode来计算hash值的，只要hashCode相同，计算出来的hash值就一样。如果存储的对象对多了，就有可能不同的对象所算出来的hash值是相同的，这就出现了所谓的hash冲突。学过数据结构的同学都知道，解决hash冲突的方法有很多，HashMap底层是通过链表来解决hash冲突的。也就是说，其链表结果主要是用来解决hash冲突的。

hashmap结构：哈希表是由数组+链表组成的，数组的默认长度为16（*可以自动变长。在构造HashMap\*的时候也可以指定一个长度**），数组里每个元素存储的是一个链表的头结点。而组成链表的结点其实就是hashmap内部定义的一个类：Entity。Entity*包含三个元素：key\*，value\*和指向下一个Entity\*的next。（https://www.cnblogs.com/xdxs/p/4982158.html）****

****![img](https://img-blog.csdn.net/2018052116182936?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
****

****
****

以上的是1.7之前的，JDK1.8中：



使用一个Node数组来存储数据，但这个Node可能是链表结构，也可能是红黑树结构

如果插入的key的hashcode相同，那么这些key也会被定位到Node数组的同一个格子里。

如果同一个格子里的key不超过8个，使用链表结构存储。

如果超过了8个，那么会调用treeifyBin函数，将链表转换为红黑树。

那么即使hashcode完全相同，由于红黑树的特定，查找某个特定元素，也只需要O(log n)的开销

也就是说put/get的操作的时间复杂度只有O(log n)

备注：当数组大小已经超过64并且链表中的元素个数超过默认设定（8个）时，将链表转化为红黑树



****
****

****下面我们来谈一下为什么要使用ConcurrentHashMap。****

****在并发编程中使用HashMap可能导致程序死循环。而使用线程安全的HashTable效率又非****常低下，基于以上两个原因，便有了ConcurrentHashMap的登场机会

****1）线程不安全的HashMap****

****在多线程环境下，使用HashMap进行put操作会引起死循环，导致CPU利用率接近100%，所以在并发情况下不能使用HashMap。HashMap在并发执行put操作时会引起死循环，是因为多线程会导致HashMap的Entry链表形成环形数据结构，一旦形成环形数据结构，Entry的next节点永远不为空，就会产生死循环获取Entry。
****

****2）效率低下的HashTable
****

****HashTable容器使用synchronized来保证线程安全，但在线程竞争激烈的情况下HashTable的效率非常低下。因为当一个线程访问HashTable的同步方法，其他线程也访问HashTable的同步方法时，会进入阻塞或轮询状态。如线程1使用put进行元素添加，线程2不但不能使用put方法添加元素，也不能使用get方法来获取元素，所以竞争越激烈效率越低。
****

****3）ConcurrentHashMap的锁分段技术可有效提升并发访问率
****

****HashTable容器在竞争激烈的并发环境下表现出效率低下的原因是所有访问HashTable的线程都必须竞争同一把锁，假如容器里有多把锁，每一把锁用于锁容器其中一部分数据，那么当多线程访问容器里不同数据段的数据时，线程间就不会存在锁竞争，从而可以有效提高并发访问效率，这就是ConcurrentHashMap所使用的锁分段技术。首先将数据分成一段一段地存储，然后给每一段数据配一把锁，当一个线程占用锁访问其中一个段数据的时候，其他段的数据也能被其他线程访问。
****

****
****

****下面我们来详细介绍一下ConcurrentHashMap的结构****

jdk1.7中采用`Segment` + `HashEntry`的方式进行实现，结构如下：

![img](https://img-blog.csdn.net/20180522145823781?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

****ConcurrentHashMap是由Segment数组结构和HashEntry数组结构组成。Segment是一种可重入锁（ReentrantLock），在ConcurrentHashMap里扮演锁的角色；HashEntry则用于存储键值对数据。一个ConcurrentHashMap里包含一个Segment数组。Segment的结构和HashMap类似，是一种数组和链表结构。一个Segment里包含一个HashEntry数组，每个HashEntry是一个链表结构的元素，每个Segment守护着一个HashEntry数组里的元素，当对HashEntry数组的数据进行修改时，必须首先获得与它对应的Segment锁，如下图所示。
****

****![img](https://img-blog.csdn.net/20180521171105146?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
****

****
****

****`ConcurrentHashMap`初始化时，计算出`Segment`数组的大小`ssize`和每个`Segment`中`HashEntry`数组的大小`cap`，并初始化`Segment`数组的第一个元素；其中`ssize`大小为2的幂次方，默认为16，`cap`大小也是2的幂次方，最小值为2，最终结果根据根据初始化容量`initialCapacity`进行计算，其中`Segment`在实现上继承了`ReentrantLock`，这样就自带了锁的功能。
****

****当执行`put`方法插入数据时，根据key的hash值，在`Segment`数组中找到相应的位置，如果相应位置的`Segment`还未初始化，则通过CAS进行赋值，接着执行`Segment`对象的`put`方法通过加锁机制插入数据。
****

****1、线程A执行`tryLock()`方法成功获取锁，则把`HashEntry`对象插入到相应的位置；
2、线程B获取锁失败，则执行`scanAndLockForPut()`方法，在`scanAndLockForPut`方法中，会通过重复执行`tryLock()`方法尝试获取锁，在多处理器环境下，重复次数为64，单处理器重复次数为1，当执行`tryLock()`方法的次数超过上限时，则执行`lock()`方法挂起线程B；
****

****3、当线程A执行完插入操作时，会通过`unlock()`方法释放锁，接着唤醒线程B继续执行；****

****
****



#### size实现

因为`ConcurrentHashMap`是可以并发插入数据的，所以在准确计算元素时存在一定的难度，一般的思路是统计每个`Segment`对象中的元素个数，然后进行累加，但是这种方式计算出来的结果并不一样的准确的，因为在计算后面几个`Segment`的元素个数时，已经计算过的`Segment`同时可能有数据的插入或则删除，在1.7的实现中，采用了如下方式：

先采用不加锁的方式，连续计算元素的个数，最多计算3次：
1、如果前后两次计算结果相同，则说明计算出来的元素个数是准确的；
2、如果前后两次计算结果都不同，则给每个`Segment`进行加锁，再计算一次元素的个数；

****
****



### 1.8实现

#### ConcurrentHashMap在1.8中的实现，相比于1.7的版本基本上全部都变掉了。首先，取消了Segment分段锁的数据结构，取而代之的是数组+链表（红黑树）的结构。而对于锁的粒度，调整为对每个数组元素加锁（Node）。然后是定位节点的hash算法被简化了，这样带来的弊端是Hash冲突会加剧。因此在链表节点数量大于8时，会将链表转化为红黑树进行存储。这样一来，查询的时间复杂度就会由原先的O(n)变为O(logN)。下面是其基本结构：

 ![img](https://img-blog.csdn.net/20180522155453418?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ltMTIzNDU2Njc3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)





1.8中放弃了`Segment`臃肿的设计，取而代之的是采用`Node` + `CAS` + `Synchronized`来保证并发安全进行实现，

只有在执行第一次`put`方法时才会调用`initTable()`初始化`Node`数组，实现如下：

```java
private final Node<K,V>[] initTable() {



    Node<K,V>[] tab; int sc;



    while ((tab = table) == null || tab.length == 0) {



        if ((sc = sizeCtl) < 0)



            Thread.yield(); // lost initialization race; just spin



        else if (U.compareAndSwapInt(this, SIZECTL, sc, -1)) {



            try {



                if ((tab = table) == null || tab.length == 0) {



                    int n = (sc > 0) ? sc : DEFAULT_CAPACITY;



                    @SuppressWarnings("unchecked")



                    Node<K,V>[] nt = (Node<K,V>[])new Node<?,?>[n];



                    table = tab = nt;



                    sc = n - (n >>> 2);



                }



            } finally {



                sizeCtl = sc;



            }



            break;



        }



    }



    return tab;



}
```

#### put实现

当执行`put`方法插入数据时，根据key的hash值，在`Node`数组中找到相应的位置，实现如下：

1、如果相应位置的`Node`还未初始化，则通过CAS插入相应的数据；

```java
else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {



    if (casTabAt(tab, i, null, new Node<K,V>(hash, key, value, null)))



        break;                   // no lock when adding to empty bin



}
```

2、如果相应位置的`Node`不为空，且当前该节点不处于移动状态，则对该节点加`synchronized`锁，如果该节点的`hash`不小于0，则遍历链表更新节点或插入新节点；

```java
if (fh >= 0) {



    binCount = 1;



    for (Node<K,V> e = f;; ++binCount) {



        K ek;



        if (e.hash == hash &&



            ((ek = e.key) == key ||



             (ek != null && key.equals(ek)))) {



            oldVal = e.val;



            if (!onlyIfAbsent)



                e.val = value;



            break;



        }



        Node<K,V> pred = e;



        if ((e = e.next) == null) {



            pred.next = new Node<K,V>(hash, key, value, null);



            break;



        }



    }



}
```

3、如果该节点是`TreeBin`类型的节点，说明是红黑树结构，则通过`putTreeVal`方法往红黑树中插入节点；

```java
else if (f instanceof TreeBin) {



    Node<K,V> p;



    binCount = 2;



    if ((p = ((TreeBin<K,V>)f).putTreeVal(hash, key, value)) != null) {



        oldVal = p.val;



        if (!onlyIfAbsent)



            p.val = value;



    }



}
```

4、如果`binCount`不为0，说明`put`操作对数据产生了影响，如果当前链表的个数达到8个，则通过`treeifyBin`方法转化为红黑树，如果`oldVal`不为空，说明是一次更新操作，没有对元素个数产生影响，则直接返回旧值；

```java
if (binCount != 0) {



    if (binCount >= TREEIFY_THRESHOLD)



        treeifyBin(tab, i);



    if (oldVal != null)



        return oldVal;



    break;



}   
```

5、如果插入的是一个新节点，则执行`addCount()`方法尝试更新元素个数`baseCount`；

#### size实现

1.8中使用一个`volatile`类型的变量`baseCount`记录元素的个数，当插入新数据或则删除数据时，会通过`addCount()`方法更新`baseCount`，实现如下：

```javascript
if ((as = counterCells) != null ||



    !U.compareAndSwapLong(this, BASECOUNT, b = baseCount, s = b + x)) {



    CounterCell a; long v; int m;



    boolean uncontended = true;



    if (as == null || (m = as.length - 1) < 0 ||



        (a = as[ThreadLocalRandom.getProbe() & m]) == null ||



        !(uncontended =



          U.compareAndSwapLong(a, CELLVALUE, v = a.value, v + x))) {



        fullAddCount(x, uncontended);



        return;



    }



    if (check <= 1)



        return;



    s = sumCount();



}
```

1、初始化时`counterCells`为空，在并发量很高时，如果存在两个线程同时执行`CAS`修改`baseCount`值，则失败的线程会继续执行方法体中的逻辑，使用`CounterCell`记录元素个数的变化；

2、如果`CounterCell`数组`counterCells`为空，调用`fullAddCount()`方法进行初始化，并插入对应的记录数，通过`CAS`设置cellsBusy字段，只有设置成功的线程才能初始化`CounterCell`数组，实现如下：

```javascript
else if (cellsBusy == 0 && counterCells == as &&



         U.compareAndSwapInt(this, CELLSBUSY, 0, 1)) {



    boolean init = false;



    try {                           // Initialize table



        if (counterCells == as) {



            CounterCell[] rs = new CounterCell[2];



            rs[h & 1] = new CounterCell(x);



            counterCells = rs;



            init = true;



        }



    } finally {



        cellsBusy = 0;



    }



    if (init)



        break;



}
```

3、如果通过`CAS`设置cellsBusy字段失败的话，则继续尝试通过`CAS`修改`baseCount`字段，如果修改`baseCount`字段成功的话，就退出循环，否则继续循环插入`CounterCell`对象；

```cpp
else if (U.compareAndSwapLong(this, BASECOUNT, v = baseCount, v + x))



    break; 
```

所以在1.8中的`size`实现比1.7简单多，因为元素个数保存`baseCount`中，部分元素的变化个数保存在`CounterCell`数组中，实现如下：

```java
public int size() {



    long n = sumCount();



    return ((n < 0L) ? 0 :



            (n > (long)Integer.MAX_VALUE) ? Integer.MAX_VALUE :



            (int)n);



}



 



final long sumCount() {



    CounterCell[] as = counterCells; CounterCell a;



    long sum = baseCount;



    if (as != null) {



        for (int i = 0; i < as.length; ++i) {



            if ((a = as[i]) != null)



                sum += a.value;



        }



    }



    return sum;



}
```

通过累加`baseCount`和`CounterCell`数组中的数量，即可得到元素的总个数；