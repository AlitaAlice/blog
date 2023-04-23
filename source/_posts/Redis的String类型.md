---
title: Redis的String类型
date: 2020-10-11 16:35:40
tags: redis
categories: redis
---

## 概述

> 本章介绍Redis的String类型

<!--more-->

## 正文

```bash
127.0.0.1:6379> set key1 v1
OK
127.0.0.1:6379> get key1
"v1"
127.0.0.1:6379> keys *
1) "myset"
2) "key1"
127.0.0.1:6379> EXISTS key1
(integer) 1
127.0.0.1:6379> append key1 "hello"  #如果当前key不存在，就相当于set key
(integer) 7
127.0.0.1:6379> get key1
"v1hello"
127.0.0.1:6379> strlen key1
(integer) 7
127.0.0.1:6379> append key1 ",alita"
(integer) 13
127.0.0.1:6379> strlen key1
(integer) 13
127.0.0.1:6379> get key1
"v1hello,alita"
```

```bash
127.0.0.1:6379> set views 0
OK
127.0.0.1:6379> get views
"0"
127.0.0.1:6379> INCR views
(integer) 1
127.0.0.1:6379> INCR views
(integer) 2
127.0.0.1:6379> get views
"2"
127.0.0.1:6379> desc views
(error) ERR unknown command `desc`, with args beginning with: `views`, 
127.0.0.1:6379> DECR views
(integer) 1
127.0.0.1:6379> get views
"1"
```

```bash
127.0.0.1:6379> DECR views
(integer) 1
127.0.0.1:6379> get views
"1"
127.0.0.1:6379> INCRBY views 10
(integer) 11
127.0.0.1:6379> get views
"11"
127.0.0.1:6379> DECRBY views 10
(integer) 1
127.0.0.1:6379> get views
"1"
```

