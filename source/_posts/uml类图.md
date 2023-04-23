---
title: uml类图
date: 2020-08-18 15:04:28
tags:
categories:
---

## 概述

> 本章介绍

<!--more-->

## 正文

# UML类图中箭头和线条的含义和用法

在学习UML过程中，你经常会遇到UML类图关系，这里就向大家介绍一下UML箭头、线条代表的意义，相信通过本文的介绍你对UML中箭头、线条的意义有更明确的认识。

AD：



本节向大家学习一下UML箭头、线条代表的意义，UML中关系主要有依赖，聚合，合成，泛化和实现等，下面就让我们来看一下这些关系如何用UML箭头和线条来实现。

UML箭头、线条程序

**关系**

后面的例子将针对某个具体目的来独立地展示各种关系。虽然语法无误，但这些例子可进一步精炼，在它们的有效范围内包括更多的语义。

**依赖（Dependency）**

实体之间一个“使用”关系暗示一个实体的规范发生变化后，可能影响依赖于它的其他实例（图D）。更具体地说，它可转换为对不在实例作用域内的一个类或对象的任何类型的引用。其中包括一个局部变量，对通过方法调用而获得的一个对象的引用（如下例所示），或者对一个类的静态方法的引用（同时不存在那个类的一个实例）。也可利用“依赖”来表示包和包之间的关系。由于包中含有类，所以你可根据那些包中的各个类之间的关系，表示出包和包的关系。

图D

[![img](http://images.51cto.com/files/uploadimg/20100617/1423350.jpg)](http://images.51cto.com/files/uploadimg/20100617/1423350.jpg)

**关联（Association）**

实体之间的一个结构化关系表明对象是相互连接的。UML箭头是可选的，它用于指定导航能力。如果没有箭头，暗示是一种双向的导航能力。在Java中，关联（图E）转换为一个实例作用域的变量，就像图E的“Java”区域所展示的代码那样。可为一个关联附加其他修饰符。多重性（Multiplicity）修饰符暗示着实例之间的关系。在示范代码中，Employee可以有0个或更多的TimeCard对象。但是，每个TimeCard只从属于单独一个Employee。

图E

[![img](http://images.51cto.com/files/uploadimg/20100617/1423351.jpg)](http://images.51cto.com/files/uploadimg/20100617/1423351.jpg)

**聚合（Aggregation）**

聚合（图F）是关联的一种形式，UML箭头代表两个类之间的整体/局部关系。聚合暗示着整体在概念上处于比局部更高的一个级别，而关联暗示两个类在概念上位于相同的级别。聚合也转换成Java中的一个实例作用域变量。7MIrrhk
yC7lR#N8j0
关联和聚合的区别纯粹是概念上的，而且严格反映在语义上。聚合还暗示着实例图中不存在回路。换言之，只能是一种单向关系。

图F

[![img](http://images.51cto.com/files/uploadimg/20100617/1423352.jpg)](http://images.51cto.com/files/uploadimg/20100617/1423352.jpg)

**合成（Composition）**

合成（图G）是聚合的一种特殊形式，UML箭头暗示“局部”在“整体”内部的生存期职责。合成也是非共享的。所以，虽然局部不一定要随整体的销毁而被销毁，但整体要么负责保持局部的存活状态，要么负责将其销毁。局部不可与其他整体共享。但是，整体可将所有权转交给另一个对象，后者随即将承担生存期职责。

Employee和TimeCard的关系或许更适合表示成“合成”，而不是表示成“关联”。

图G

[![img](http://images.51cto.com/files/uploadimg/20100617/1423353.jpg)](http://images.51cto.com/files/uploadimg/20100617/1423353.jpg)

**泛化（Generalization）**

泛化（图H）表示一个更泛化的元素和一个更具体的元素之间的关系。泛化是用于对继承进行建模的UML元素。在Java中，用extends关键字来直接表示这种关系。

图H

[![img](http://images.51cto.com/files/uploadimg/20100617/1423354.jpg)](http://images.51cto.com/files/uploadimg/20100617/1423354.jpg)

**实现（Realization）**

实例（图I）关系UML箭头指定两个实体之间的一个合同。换言之，一个实体定义一个合同，而另一个实体保证履行该合同。对Java应用程序进行建模时，实现关系可直接用implements关键字来表示。

图I

[![img](http://images.51cto.com/files/uploadimg/20100617/1423355.jpg)](http://images.51cto.com/files/uploadimg/20100617/1423355.jpg)