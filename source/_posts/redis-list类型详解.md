---
title: redis_list类型详解
date: 2020-08-18 11:09:39
tags: redis
categories: redis
---

## 概述

> 本章介绍redis_list类型详解

<!--more-->

## 正文

```bash
127.0.0.1:6379> LPUSH list one   #将一个值或者多个值，插入到列表头部
(integer) 1
127.0.0.1:6379> LPUSH list two
(integer) 2
127.0.0.1:6379> lpush list three
(integer) 3
127.0.0.1:6379> lrange list 0 -1
1) "three"
2) "two"
3) "one"
127.0.0.1:6379> lrange list 0 1
1) "three"
2) "two"
127.0.0.1:6379> rpush list right   #从右侧插入list
(integer) 4
127.0.0.1:6379> LRANGE list 0 -1
1) "three"
2) "two"
3) "one"
4) "right"
```

```bash
127.0.0.1:6379> lrange list 0 -1
1) "three"
2) "two"
3) "one"
4) "right"
127.0.0.1:6379> lpop list 
"three"
127.0.0.1:6379> rpop list
"right"
127.0.0.1:6379> LRANGE list 0 -1
1) "two"
2) "one"
```

```bash
127.0.0.1:6379> lindex list 1    #通过下标来获取list中的某一个值
"one"
127.0.0.1:6379> lindex list 0   
"two"
127.0.0.1:6379> llen list   #返回列表的长度
(integer) 2 
```

```bash
127.0.0.1:6379> lrange list 0 -1
1) "two"
2) "one"
3) "two"
4) "one"
127.0.0.1:6379> lrem list 1 two   #移除指定元素
(integer) 1
127.0.0.1:6379> lrem list 2 one 
(integer) 2
127.0.0.1:6379> lrange list 0 -1
1) "two"
```

```bash
127.0.0.1:6379> Rpush mylist "hello"
(integer) 1
127.0.0.1:6379> Rpush mylist "hello1"
(integer) 2
127.0.0.1:6379> Rpush mylist "hello2"
(integer) 3
127.0.0.1:6379> Rpush mylist "hello3"
(integer) 4
127.0.0.1:6379> Rpush mylist "hello4"
(integer) 5
127.0.0.1:6379> LTRIM mylist 1 2  #通过下标截取指定长度
OK
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello1"
2) "hello2"
```

```bash
127.0.0.1:6379> rpoplpush mylist mylist2  #rpop 后lpush
"hello2"
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello1"
127.0.0.1:6379> LRANGE mylist2 0 -1
1) "hello2"
```

```bash
127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello1"
127.0.0.1:6379> lset list 0 item     #lset命令 将指定index替换
(error) ERR no such key
127.0.0.1:6379> lset mylist 0 item
OK
127.0.0.1:6379> LRANGE mylist 0 -1
1) "item"
```

```bash
127.0.0.1:6379> LRANGE mylist 0 -1
1) "item"
127.0.0.1:6379> lpush mylist hello
(integer) 2
127.0.0.1:6379> lrange mylist 0 -1
1) "hello"
2) "item"
127.0.0.1:6379> LINSERT mylist  after "hello" world  #linsert 在指定字符串前/后 插入
(integer) 3
127.0.0.1:6379> lrange mylist 0 -1
1) "hello"
2) "world"
3) "item"
```

