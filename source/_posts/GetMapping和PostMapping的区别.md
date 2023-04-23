---
title: GetMapping和PostMapping的区别
date: 2020-06-29 15:41:41
tags: springboot
categories: springboot
---

## 概述

> 本章介绍GetMapping和PostMapping的区别

<!--more-->

## 正文

最近刚学完三大框架，回过头来做东西发现很多东西都忘了，GET\POST是有区别的
spring4.3中引进了｛@GetMapping、@PostMapping、@PutMapping、@DeleteMapping、@PatchMapping｝，来帮助简化常用的HTTP方法的映射，并更好地表达被注解方法的语义。
以@GetMapping为例，Spring官方文档说：
@GetMapping是一个组合注解，是@RequestMapping(method = RequestMethod.GET)的缩写。该注解将HTTP Get 映射到 特定的处理方法上。

以下是官方解释，供大家参考：

哪一些情况下，浏览器会发送get请求

1. 直接在浏览器地址栏输入某个地址

2. 点击链接

3. 表单默认的提交方式

哪一些情况下，浏览器会发送post请求？

1. 设置表单method = “post”

get请求的特点

1. 请求参数会添加到请求资源路劲的后面，只能添加少量参数（因为请求行只有一行，大约只能存放2K左右的数据）（2K左右的数据，看起来也不少。。。）

2. 请求参数会显示在浏览器地址栏，路由器会记录请求地址

post请求的特点

1. 请求参数添加到实体内容里面，可以添加大量的参数（也解释了为什么浏览器地址栏不能发送post请求，在地址栏里我们只能填写URL，并不能进入到Http包的实体当中）

2. 相对安全，但是，post请求不会对请求参数进行加密处理（可以使用https协议来保证数据安全）。
   