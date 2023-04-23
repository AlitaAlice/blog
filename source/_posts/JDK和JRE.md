---
title: JDK和JRE
date: 2020-05-09 11:11:39
tags: JAVASE
categories: 后端
---

## 概述

> 本章介绍JDK和JRE的区别，他们的作用分别是什么？

<!--more-->

## 正文

## JDK

JDK是JAVA Development Kit (JAVA开发套件) ，是JAVA的开发工具包。主要包含了类库和工具。

JDK中包含了JRE 而且在JDK安装目录/JRE/bin/server 文件夹下包含jvm.dll

![](QQ20200509115538.png)

这说明JDK提供了一个虚拟机。

另外JDK的bin目录下有各种JAVA程序需要用到的命令。

与JRE明显的区别就是JDK文件下才会有javac

![](QQ20200509115836.png)

因为JRE只是一个运行环境，与开发无关。

## JRE

JRE是JAVA Runtime Environment的缩写。是JAVA程序的运行环境。既然是运行，那么当然要包含JVM,也就是JAVA虚拟机，还有所有JAVA类库的class文件，都在lib下，并且被打包成了jar 

![](Screenshot.png)

## 问题：jdk里的jre与外面jre的区别

分析：如果我们安装了JDK，那么我们的电脑中将会有C:\Program Files (x86)\Java\jdk1.8.0_05文件夹 ，这个文件夹里面有一个jre文件夹。然后我们再安装jre，此时我们的电脑中有C:\Program Files (x86)\Java\jre8文件夹。

通过对比jre和jre8文件夹中的东西，我们发现基本是一样的，那么这俩文件夹到底有啥区别呢？

我们暂且称jre为自带jdk-jre，jre8为公共jre。

jdk-jre与公共jre的主要区别在于jdk-jre多了一个server的vm执行选项。

sever与client使用不同的vm虚拟机。如果电脑运行一个java程序的时候，会自动调用client vm。但是如果开发java程序时使用的就是server vm（server vm启动时间较长，占用内存较多，但是启动后执行性能更高，适合开发）。

**换句话说：公共jre是给普通电脑用户使用的，假如你安装了一个java程序，这个java程序启动运行的时候就会调用jre（java runtime environment）；如果你是一个java开发者，那么你就需要安装jdk（java development kit），这时你开发调试java程序的时候就会调用jdk里面的jre。**