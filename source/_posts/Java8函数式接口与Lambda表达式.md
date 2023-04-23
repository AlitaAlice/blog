---
title: Java8函数式接口与lambda表达式
date: 2020-05-28 11:18:17
tags: JAVASE
categories: JAVASE
---

## 概述

> 本章介绍lambda

<!--more-->

## 正文

转自https://blog.csdn.net/justloveyou_/article/details/89066782

## lambda表达式

lambda表达式采用一种简洁的语法来定义代码块。lambda表达式是一个可传递的代码块，可以在以后执行一次或者多次。

eg:

```java
class LengthComparator implements Comparator<String>
{
public int compare(String first,String second)
{
return first.length()-senond.length;
}
}
...
Arrays.sort(strings,new LenthComparator());
在JAVA中传递一个代码段并不容易，你不能直接传递代码段，JAVA是一种面向对象的语言，所以必须构造一个对象，这个对象的类需要有一个方法来包含所必须的代码段。
```

## lambda表达式的语法

```java
(String first,String second)
->first.length()-second.length()
这是一个lambda表达式，lambda表达式是一个代码块，以及必须传入代码的变量规范，
```

```java
(String first,String second)->
{
  if(first.length() <second.length() return -1;
  if(first.length() >second.length() return 1;
  else return 0;
  )
}
以上包含显式的return 语句
```

```java
即使lambda表达式没有参数，仍然要提供空括号
()->{for (int i=100;i>=0;i--) System.out.println(i);}
```

```java
如果可以推导出一个lambda表达式的参数类型，则可以忽略其类型。
Comparator<String> compatator=(first,second) ->first.length()-second.length();
```

```java
如果方法只有一个参数，并且这个参数的类型可以推导得出，那么甚至可以省略括号
ActionListener listener =event ->System.out.println("this time is" +Instant.ofEpochMilli(event.getWhen()));
instead of (event)->...or(ActionEvent event)->
```

