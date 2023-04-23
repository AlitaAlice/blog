---
title: JAVA内存区域与内存溢出异常
date: 2020-05-15 17:05:29
tags: JVM
categories: JVM
---

## 概述

> 本章介绍JAVA内存区域与内存溢出异常

<!--more-->

## 正文

类文件(`.class`文件扩展名)是包含Java字节码 `ByteCode`的文件，可以在Java虚拟机上执行，每个类文件包含了一个类，接口或者模块（Java 9）的定义.Java程序（`.java` 文件）可以通过 Java compiler 生成字节码文件，其他基于JVM的语言也都可以通过自己的编译器生成字节码文件，例如Scala，Groovy等JVM是与平台无关的，类文件可以在多个平台上执行，这使得相应的语言也与平台无关.

## JVM的内存布局

虚拟机中，Java 内存区域可以划分为 6 个部分，程序计数器、虚拟机栈、本地方法栈（以上三个是线程私有的）、堆和方法区（里面有常量池，方法区与堆是线程共享的 )、直接内存（不受 JVM GC 管理）。除了直接内存，其他都是运行时数据区。

![](https://photos.alitaalice.cn/image/20200517164736.png)

## 对象的创建

![](https://photos.alitaalice.cn/image/20200517165000.png)

![](https://photos.alitaalice.cn/image/20200517165050.png)

## 对象的内存布局

![](https://photos.alitaalice.cn/image/20200517164220.png)

![](https://photos.alitaalice.cn/image/20200517165147.png)

![](https://photos.alitaalice.cn/image/20200517165221.png)

![](https://photos.alitaalice.cn/image/20200517165249.png)

![](https://photos.alitaalice.cn/image/20200517165303.png)