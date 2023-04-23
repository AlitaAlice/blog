---
title: JDK7和JDK8的区别
date: 2020-05-29 22:01:16
tags: JAVASE
categories: JAVASE
---

## 概述

> 本章介绍JDK7和JDK8的区别

<!--more-->

## 正文

## **JDK 7**

1. 对集合类的语言支持；
2. try-with-resources 语句
3. 使用文件 Path
4. 改进的通用实例创建类型推断；(？？)
5. 数字字面量下划线支持；（√）
6. switch中使用string；（√）
7. 二进制字面量；（√）
8. 简化可变参数方法调用。
9. map集合支持并发请求 ，且可以写成 Map map = {name:”xxx”,age:18};
10. Boolean类型反转，空指针安全,参与位运算；
11. 新增一些取环境信息的工具方法；

## JDK 8

1、**接口可以添加默认方法，default;**
2、**lambda表达式，对于接口可以直接用()->{}方式来表达，小括号表示方法入参，花括号内表示方法返回值，如Collections的sort()方法**：
3、**函数式接口**
4、新的日期和时间API
5、并发增强
6、支持多重注解
7、**特性四、反射的加强 。JDK8加强了反射，它允许你直接通过反射获取参数的名字**
8、 **Stream API** 

Java 8 API添加了一个新的抽象称为流Stream，可以让你以一种声明的方式处理数据。

Stream 使用一种类似用 SQL 语句从数据库查询数据的直观方式来提供一种对 Java 集合运算和表达的高阶抽象。

Stream API可以极大提高Java程序员的生产力，让程序员写出高效率、干净、简洁的代码。 9、  JavaScript引擎Nashorn
10、Java虚拟机（JVM）的新特性
PermGen空间被移除了，取而代之的是Metaspace（JEP 122）。JVM选项-XX:PermSize与-XX:MaxPermSize分别被-XX:MetaSpaceSize与-XX:MaxMetaspaceSize所代替。