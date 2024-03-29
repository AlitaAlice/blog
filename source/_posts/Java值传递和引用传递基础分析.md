---
title: Java值传递和引用传递基础分析
date: 2020-05-11 12:13:37
tags: JAVASE
categories: 面试
---

## 概述

> 本章介绍JAVA的值传递和引用传递

<!--more-->

## 正文

## java内的基础类型数据传递都是值传递. java中实例对象的传递是引用传递。

**值传递是对基本型变量而言的,传递的是该变量的一个副本,改变副本不影响原变量。引用传递一般是对于对象型变量而言的,传递的是该对象地址的一个副本, 并不是原对象本身 。**

首先，不要纠结于 Pass By Value 和 Pass By Reference 的字面上的意义，否则很容易陷入所谓的“一切传引用其实本质上是传值”这种并不能解决问题无意义论战中。
更何况，要想知道Java到底是传值还是传引用，起码你要先知道传值和传引用的准确含义吧？可是如果你已经知道了这两个名字的准确含义，那么你自己就能判断Java到底是传值还是传引用。

## 一：搞清楚 基本类型 和 引用类型的不同之处

```java
int num = 10;
String str = "hello";
```

![](2020-05-12_112353.png)

如图所示，num是基本类型，值就直接保存在变量中。而str是引用类型，变量中保存的只是实际对象的地址。一般称这种变量为"引用"，引用指向实际对象，实际对象中保存着内容。

二：搞清楚赋值运算符（=）的作用

```
num = 20;
str = "java";
```

对于基本类型 num ，赋值运算符会直接改变变量的值，原来的值被覆盖掉。
对于引用类型 str，赋值运算符会改变引用中所保存的地址，原来的地址被覆盖掉。但是原来的对象不会被改变（重要）。
如上图所示，"hello" 字符串对象没有被改变。（没有被任何引用所指向的对象是垃圾，会被垃圾回收器回收）

![](2020-05-12_112409.png)

## 三：调用方法时发生了什么？参数传递基本上就是赋值操作

第一个例子：基本类型

```java
void foo(int value) {

    value = 100;

}
foo(num); // num 没有被改变
```

第二个例子：没有提供改变自身方法的引用类型

```java
void foo(String text) {
    text = "windows";  //String没改变是因为赋值新的字符串直接导致新new了一个String
}
foo(str); // str 也没有被改变
```

第三个例子：提供改变自身方法的引用类型

builder的引用对象也是StringBuilder

```java
StringBuilder sb = new StringBuilder("iphone");

void foo(StringBuilder builder) {

    builder.append("4"); //没有生成新的stringBuilder对象

}
foo(sb); // sb 被改变了，变成了"iphone4"。
```

第四个例子：提供了改变自身方法的引用类型，但是不使用，而是使用赋值运算符。

```java
StringBuilder sb = new StringBuilder("iphone");

void foo(StringBuilder builder) {

    builder = new StringBuilder("ipad");
}

foo(sb); // sb 没有被改变，还是 "iphone"。
```

重点理解为什么，第三个例子和第四个例子结果不同？

下面是第三个例子的图解：

![](2020-05-12_112424.png)

builder = new StringBuilder("ipad"); 之后

![](2020-05-12_112435.png)