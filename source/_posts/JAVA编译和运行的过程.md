---
title: JAVA编译和运行的过程
date: 2020-05-11 16:18:28
tags: JAVASE
categories: 后端
---

## 概述

> 本章介绍JAVA编译和运行的过程

<!--more-->

## 正文

- JAVA程序源码 

- -------> JAVA字节码（经过编译器编译)

- ------->JVM （对字节码进行解释和运行）

  编译只进行一次，但是解释在每次运行程序时都会运行，编译的字节码采用一种针对JVM优化过度机器码的形式进行保存

- ------>机器码（虚拟机将字节码解释为机器码，在计算机上运行）

  ![](Screenshot.png)

