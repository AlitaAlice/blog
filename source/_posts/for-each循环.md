---
title: for_each循环
date: 2020-05-29 15:07:26
tags: JAVASE
categories: JAVASE
---

## 概述

> 本章介绍for_each循环

<!--more-->

## 正文

for(variable :collection)  statement

它定义一个变量用于暂存集合中的每一个元素。

但是collection必须是一个数组或者一个实现了Iterable接口的类对象（例如ArrayList)

eg:

```java
for(int element :a)
    System.out.println(element);
```

这个循环应该读作 循环a中的每一个元素。

在for_each 循环语句中的循环变量将会遍历循环数组中的每个元素，而不是下标值。