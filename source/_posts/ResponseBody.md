---
title: '@ResponseBody'
date: 2020-07-28 21:50:27
tags:
categories:
---

## 概述

> 本章介绍

<!--more-->

## 正文

@ResponseBody是作用在方法上的，@ResponseBody 表示该方法的返回结果直接写入 HTTP response body 中，一般在异步获取数据时使用【也就是AJAX】，在使用 @RequestMapping后，返回值通常解析为跳转路径，但是加上 @ResponseBody 后返回结果不会被解析为跳转路径，而是直接写入 HTTP response body 中。 比如异步获取 json 数据，加上 @ResponseBody 后，会直接返回 json 数据。@RequestBody 将 HTTP 请求正文插入方法中，使用适合的 HttpMessageConverter 将请求体写入某个对象。

 在使用springmvc框架的时候，在处理json的时候需要用到spring框架特有的注解@ResponseBody或者@RestController注解，这两个注解都会处理返回的数据格式，使用了该类型注解后返回的不再是视图，不会进行转跳，而是返回json或xml数据格式，输出在页面上。



  那么，这两个注解在使用上有什么区别呢？

  @ResponseBody，一般是使用在单独的方法上的，需要哪个方法返回json数据格式，就在哪个方法上使用，具有针对性。

  @RestController，一般是使用在类上的，它表示的意思其实就是结合了@Controller和@ResponseBody两个注解，

如果哪个类下的所有方法需要返回json数据格式的，就在哪个类上使用该注解，具有统一性；需要注意的是，使用了@RestController注解之后，其本质相当于在该类的所有方法上都统一使用了@ResponseBody注解，所以该类下的所有方法都会返回json数据格式，输出在页面上，而不会再返回视图。