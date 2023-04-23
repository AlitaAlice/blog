---
title: SpringMVC流程
date: 2020-06-15 09:18:49
tags: SpringMVC
categories: SpringMVC
---

## 概述

> 本章介绍SpringMVC流程

<!--more-->

## 正文

SpringMVC流程：请求执行到后端控制器（位于Web层）之后，后端控制器会继续调用Service层中的业务代码，而Service层继续向后调用Manager层或者DAO层，进而获得目标数据。Service层将获得到的目标数据返回给后端控制器。后端控制器把目标数据包装成Model之后返回给ViewResolver，ViewResolver把Model渲染成最终用户看到的页面。

![](https://photos.alitaalice.cn/image/20200615092105.png)

![image-20200615092208397](C:\Users\16508\AppData\Roaming\Typora\typora-user-images\image-20200615092208397.png)

![](https://photos.alitaalice.cn/image/20200615092336.png)