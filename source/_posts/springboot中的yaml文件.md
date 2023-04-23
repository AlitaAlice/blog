---
title: springboot中的yaml文件
date: 2020-10-09 19:29:55
tags: springboot
categories: springboot
---

## 概述

> 本章介绍springboot中的yaml文件

<!--more-->

## 正文

```java
spring:
profiles:
  active: dev
```

使用spring.profiles指定环境标识，例如dev环境、test环境。使用spring.profiles.active指定生效的环境配置