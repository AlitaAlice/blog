---
title: java8的常用特性
date: 2021-02-14 13:48:31
tags: javase
categories: javase
---

## 概述

> 本章介绍java8的常用特性

<!--more-->

## 正文

## 1 方法引用

1 构造器引用

```
Class::new
```

2 静态方法引用

```
Class::static_method
```

3 方法引用的类型是某个类的成员方法的引用

```
Class::method
```

4 方法引用的类型是某个类的成员方法的引用

```
instance::method
```

## 2 函数式编程

![](https://photos.alitaalice.cn/image/20210214140544.png)

## 3 Map新增方法

**putIfAbsent**  如果传入key对应的value已经存在，就返回存在的value，不进行替换。如果不存在，就添加key和value，返回null

```java
map中compute，computeIfAbsent，computeIfPresent方法介绍
1 compute的方法,指定的key在map中的值进行操作 不管存不存在，操作完成后保存到map中
 Integer integer = map.compute("3", (k,v) -> v+1 );
2 computeIfAbsent的方法有两个参数 第一个是所选map的key，第二个是需要做的操作。这个方法当key值不存在时才起作用。
Integer integer = map.computeIfAbsent("3", key -> new Integer(4));
3 computeIfPresent 的方法,对 指定的 在map中已经存在的key的value进行操作。只对已经存在key的进行操作，其他不操作
 Integer integer = map.computeIfPresent("3", (k,v) -> v+1 );
```

## 4 stream

**1 Reduce 规约**

这是一个最终操作，允许通过指定的函数来讲stream中的多个元素规约为一个元素，规越后的结果是通过Optional接口表示的：

代码如下:

```
Optional<String> reduced =
    stringCollection
        .stream()
        .sorted()
        .reduce((s1, s2) -> s1 + "#" + s2);
reduced.ifPresent(System.out::println);
// "aaa1#aaa2#bbb1#bbb2#bbb3#ccc#ddd1#ddd2"
```

**2 flatMap提取子流**

.flatMap(Arrays::stream)

.flatMap(Collection::stream)

## 5 Optional

![](https://photos.alitaalice.cn/image/20210214141327.png)

使用示例：

