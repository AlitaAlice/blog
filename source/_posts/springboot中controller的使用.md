---
title: springboot中controller的使用
date: 2020-06-12 19:41:53
tags: springboot
categories: springboot
---

## 概述

> 本章介绍springboot中controller的使用

<!--more-->

## 正文

1 

![](https://photos.alitaalice.cn/image/20200613091901.png)

![](https://photos.alitaalice.cn/image/20200613092010.png)

![image-20200613092031562](C:\Users\16508\AppData\Roaming\Typora\typora-user-images\image-20200613092031562.png)

![](https://photos.alitaalice.cn/image/20200613092049.png)

![](https://photos.alitaalice.cn/image/20200613092100.png)-

# @RequestBody

@RequestBody主要用来json转换为java对象。 前台向后台传数据

@ResponseBody的作用其实是将java对象转为json格式的数据。后台传前台。

# model.attribute()的作用

1.往前台传数据，可以传对象，可以传List，通过el表达式 ${}可以获取到，

类似于request.setAttribute("sts",sts)效果一样。

2.@ModelAttribute("model")  注解