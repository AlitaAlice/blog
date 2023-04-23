---
title: Nosql
date: 2020-08-15 10:05:07
tags:
categories:
---

## 概述

> 本章介绍

<!--more-->

## 正文



>NOSQL 的特点	

1 方便扩展（数据之间没有关系，很好扩展）

2 大数据量高性能(Redis 读11W 写 8W  ，Nosql的缓存记录及，是一种细粒度的缓存，性能比较高)

3 数据类型是多样型的（不需要事先设计数据库！随取随用，如果是数据量十分大的表，很多人无法设计了）

![](https://photos.alitaalice.cn/image/20200815100825.png)

4 传统RDBMS和NOSQL的区别

```
 传统的RDBMS
 -结构化组织
 sql
 数据和关系存在单独的表中 row column
 操作操作，数据定义语言 
 严格的一致性
 基础的事务
 ...
```

```
nosql
-不仅仅是数据
-没有固定的查询语言
-键值对存储，列存储，文档存储，图形数据库
-最终一致性
-CAP定理 和BASE（异地多活） 
-高性能高可用高可扩
```



>了解：3V+3高



![](https://photos.alitaalice.cn/image/20200815101725.png)

真正在公司中的实践：NOSQL+RDBMS

## 阿里巴巴演进分析

![](https://photos.alitaalice.cn/image/20200815103607.png)

![](https://photos.alitaalice.cn/image/20200815103826.png) 



### NOSqL的四大分类

![](https://photos.alitaalice.cn/image/20200815105535.png)

![](https://photos.alitaalice.cn/image/20200815105609.png)

他不是存储图形的，放的是关系，比如朋友圈社交网络，广告推荐0

## 理解

![](https://photos.alitaalice.cn/image/20200815105745.png) 

### Redis入门

>
>
>redis是什么？

Remote Dictionary Server 远程字典服务  

key-value数据库 

并提供多种语言的API

最热门的NOSQL技术之一  也被人们称为结构化数据库

![](https://photos.alitaalice.cn/image/20200815160754.png)



![](https://photos.alitaalice.cn/image/20200815160856.png)

### windows安装

![](https://photos.alitaalice.cn/image/20200815162024.png)

推荐使用linux学习



### linux安装