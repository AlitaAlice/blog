---
title: List接口
date: 2020-05-07 11:12:17
tags: JAVA集合
categories: JAVA集合
---

## 概述

> List集合包括List接口和List接口所有的实现类

<!--more-->

## 正文

## List接口定义的方法

除了继承Collection外，List接口还有俩个重要的方法。

| get(int index)            | 获得指定索引位置的元素                     |
| ------------------------- | ------------------------------------------ |
| set(int index,Object obj) | 将集合中指定索引位置的对象修改为指定的对象 |

## List接口的实现类

- ArrayList

  实现了可变的数组，允许保存所有元素包括null .并且可以根据索引的位置对集合进行快速的随机访问，缺点是向指向的索引位置插入对象或删除对象时的速度较慢

- LinkedList 

  采用链表的结构保存对象。优点是便于向集合中插入和删除对象
  
  分别用ArrayList 和LinkedList来实例化集合
  
  ```java
  List<E> list=new ArrayList<>();
  List<E> list=new LinkedList<>();
  ```
  
  E是合法的JAVA数据类型，也可以是字符串String
  
  
