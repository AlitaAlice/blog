---
title: JVM初探
date: 2020-09-01 22:54:16
tags: JVM
categories: JVM
---

## 概述

> 本章介绍

<!--more-->

## 正文

![](https://photos.alitaalice.cn/image/20200901225519.png)

- ![](https://photos.alitaalice.cn/image/20200901225829.png)


#        基本概念

![](https://photos.alitaalice.cn/image/20200901230041.png)

 1

![](https://photos.alitaalice.cn/image/20200902090342.png)

# 2  JVM模型![](https://photos.alitaalice.cn/image/20200902090937.png)

![](https://photos.alitaalice.cn/image/20200902091021.png)

# 3.类加载器：

## 如何new一个文件？

加载Class文件  经过class loader 创建class模板 根据class模板再去统一创建实例对象



![](https://photos.alitaalice.cn/image/20200902092146.png)

# 类加载器的分类

1 应用程序加载器   AppClassLoader

2 扩展类加载器   ExtClassLoader

3 启动类（根）加载器  Root

4 虚拟机自带的加载器

5 类加载器的双亲委派机制



![](https://photos.alitaalice.cn/image/20200902093939.png)

![](https://photos.alitaalice.cn/image/20200902094216.png)

5.  # 沙箱安全机制

![](https://photos.alitaalice.cn/image/20200902095820.png)

![](https://photos.alitaalice.cn/image/20200902095925.png)

6. # Native关键字

   ![](https://photos.alitaalice.cn/image/20200902100616.png)

7 ![](https://photos.alitaalice.cn/image/20200902101021.png)

![](https://photos.alitaalice.cn/image/20200902102517.png)

String类型的赋值放在常量池中

String.intern()

尽管在输出中调用intern方法并没有什么效果，但是实际上后台这个方法会做一系列的动作和操作。在调用”ab”.intern()方法的时候会返回”ab”，但是这个方法会首先检查字符串池中是否有”ab”这个字符串，如果存在则返回这个字符串的引用，否则就将这个字符串添加到字符串池中，然会返回这个字符串的引用。



9 ![](https://photos.alitaalice.cn/image/20200902104147.png)

 

![](https://photos.alitaalice.cn/image/20200902104531.png)

![](https://photos.alitaalice.cn/image/20200902105001.png)



### New对象

![](https://photos.alitaalice.cn/image/20200902222748.png)

## 3种JVM

栈是线程级别的

![](https://photos.alitaalice.cn/image/20200902223356.png)

# 堆（Heap）

![](https://photos.alitaalice.cn/image/20200903095800.png)

在JAVA1.8中永久存储区上升到元空间

**常量(字符串常量和基本类型常量)通常直接存储在程序代码内部（常量池）**

![](https://photos.alitaalice.cn/image/20200903100927.png)

GC垃圾回收，主要在伊甸园区和养老区

假设内存满了，OOM，堆内存不够

![](https://photos.alitaalice.cn/image/20200903100824.png)

# 新生区

![](https://photos.alitaalice.cn/image/20200903150323.png)

![](https://photos.alitaalice.cn/image/20200903151013.png)

![](https://photos.alitaalice.cn/image/20200903151401.png)

![](https://photos.alitaalice.cn/image/20200903151701.png)

![](https://photos.alitaalice.cn/image/20200903155605.png)

#### 元空间 逻辑上存在，物理上不存在

![](https://photos.alitaalice.cn/image/20200903160153.png)

![](https://photos.alitaalice.cn/image/20200903160434.png)

StackOverflowError异常  递归调用函数， 线程栈溢出：通过大量的递归调用来消耗线程栈内存。

# JVM参数

1 Xms JVM初始大小   Xmx 总大小

产生Dump文件 

- VM options -Xms1m -Xmx8m -XX: +HeapDumpOutOfMemoryError

后在代码目录下找到Dump文件，使用Jprofiler来分析，快速定位内存泄漏

# GC：垃圾回收

![](https://photos.alitaalice.cn/image/20200906133926.png)

yin