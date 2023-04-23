---
title: char可以存储汉字吗？
date: 2020-05-06 09:51:17
tags: JAVASE
categories: JAVASE
---

## char存储汉字

- char是按照字符存储的，不管是英文还是中文，JAVA中固定占用2个字符，用来存储Unicode字符，范围在0-65535.

- Unicode编码字符集中包含了汉字，所以char类型变量当然可以存储汉字拉。
  <!--more-->

  ## char和String的区别

  - char表示字符，定义时用单引号，只能存储一个字符。如char c=‘x’ ;
  - String表示的是字符串，可以存储一个或多个字符 如String name="tom";
  - 


如name.length();