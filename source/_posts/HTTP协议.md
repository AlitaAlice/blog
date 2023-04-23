---
title: HTTP协议
date: 2020-05-18 11:09:22
tags: HTTP
categories: HTTP
---

## 概述

> 本章介绍HTTP协议

<!--more-->

## 正文

### 1 HTTP 协议用于客户端和服务器端之间的通信  

HTTP 协议能够明确区分哪端是客户端，哪端是服务器端  

### 2 通过请求和响应的交换达成通信  

HTTP 协议规定，请求从客户端发出，最后服务器端响应该请求并返回  

![](https://photos.alitaalice.cn/image/20200518114122.png)

起始行开头的GET表示请求访问服务器的类型，称为方法（method）。随后的字符串 /index.htm 指明了请求访问的资源对象，也叫做请求 URI（request-URI）。最后的 HTTP/1.1，即 HTTP 的版本号，用来提示客户端使用的 HTTP 协议功能  .

请求首部字段及内容实体稍后会作详细说明。接下来，我们继续讲解。接收到请求的服务器，会将请求内容的处理结果以响应的形式返回。  

![](https://photos.alitaalice.cn/image/20200518114432.png)

![](https://photos.alitaalice.cn/image/20200518114521.png)

### 3 HTTP 是不保存状态的协议  

HTTP 是一种不保存状态，即无状态（stateless）协议。HTTP 协议自身不对请求和响应之间的通信状态进行保存。也就是说在 HTTP 这个级别，协议对于发送过的请求或响应都不做持久化处理。  

![](https://photos.alitaalice.cn/image/20200518114709.png)

### 4 请求URI定位资源

![](https://photos.alitaalice.cn/image/20200518115112.png)

### 5 HTTP方法 

![](https://photos.alitaalice.cn/image/20200518164346.png)

### 6 持久连接

持久连接的特点是，只要任意一端没有明确提出断开连接，则保持 TCP 连接状态，持久连接旨在建立 1 次 TCP 连接后进行多次请求和响应的交互。

### 7 管线化

持久连接使得多数请求以管线化（pipelining）方式发送成为可能。从前发送请求后需等待并收到响应，才能发送下一个请求。管线化技术出现后，不用等待响应亦可直接发送下一个请求。
这样就能够做到同时并行发送多个请求，而不需要一个接一个地等待响应了。  

![](https://photos.alitaalice.cn/image/20200518164857.png)

### 8 使用Cookie的状态管理

![](https://photos.alitaalice.cn/image/20200518165228.png)



### 各层对应的协议

### OSI七层对各层协议