---
title: Arrays类相关
date: 2020-05-29 15:36:17
tags: JAVASE
categories: JAVASE
---

## 概述

> 本章介绍Arrays类相关.

<!--more-->

## 正文

转https://blog.csdn.net/LIU_YANZHAO/article/details/70847050?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase

# java List和数组相互转换方法

### 1 List转数组

####  toArray()方法

```java
  List<String> list = new ArrayList<String>();
        list.add("1");
        String[] strings = new String[list.size()];
        list.toArray(strings);
        System.out.println(strings);
        System.out.println(strings.getClass());
        System.out.println(Arrays.toString(strings));
```

### 2 数组转List

#### 使用asList（）

```java
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(arrays));
```