---
title: JAVA_String_API
date: 2020-05-06 22:12:33
tags: JAVASE
categories: JAVASE
---

String API

- append()


  在由许多小段的字符串构建一个字符串时，则使用StringBuilder类（字符串构造器）

  首先构造一个空的字符串构造器：
  <!--more-->

  ```java
  StringBuilder builder =new StringBuilder(); 	
  ```

  当需要添加一部分内容时，调用append()方法

  ```java
  builder.append(ch);
  builder.append(str);
  String completedString=builder.toString(); /*调用toString()方法，得到String对象。*/
  ```

- char charAt(int index)

  返回给定位置的代码单元。

- int length()

​         返回字符串代码单元的个数

- String repeat(int count)

  返回一个字符串，将当前字符重复count次

- boolean equals() 

  用来检测俩个字符串是否相等

  boolean equalsIgnoreCase() 

  用来检测俩个字符串是否相等（不区分大小写）

  ```java
  "hello".equals(greeting);
  "HELLO".equalsIgnoreCase("hello"); /* 不区分大小写 */  
  ```

-  注意：

  **不要用==运算符检测是否相等。**

  **这个运算符只能够确定俩个字符串是否存放在同一个位置上。**当然如果字符串存放在同一个位置上，它们必然相等，但是完全有可能把内容相同的多个字符串副本放置在不同的位置上。

  ```java
  String greeting="Hello";
  if(greeting =="Hello")
    -- true
   if(greeting.substring(0,3)=="Hel")
    --false
  ```

  实际上只有字符串字面量共享，而+或者substring操作得到的字符串并不共享。

  

