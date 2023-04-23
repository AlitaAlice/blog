---
title: redis
date: 2020-08-15 19:49:30
tags: nosql
categories: nosql
---

## 概述

> 本章介绍redis

<!--more-->

## 正文

## 测试性能

redis-benchmark

![](https://photos.alitaalice.cn/image/20200815195127.png)

```

```

默认16个数据库

![](https://photos.alitaalice.cn/image/20200815200339.png)

```
查看所有的key
keys *
清除当前数据库
flushdb
清除所有数据库
flushall
```

>
>
>redis 是单线程的！
>
>

redis是很快的，Redis是基于内存操作，cpu不少redis性能瓶颈

redis的瓶颈是根据机器的内存和网络带宽

既然可以使用单线程 就使用单线程 

>Redis 为什么单线程还那么快

> ![](https://photos.alitaalice.cn/image/20200815210502.png)
>

对于内存系统来说，如果没有上下文切换效率是最高的，多次读写都是在一个CPU上的，在内存情况上，这个是最佳的方案。

 

![](https://photos.alitaalice.cn/image/20200816094836.png)

![](https://photos.alitaalice.cn/image/20200816095704.png)

![](https://photos.alitaalice.cn/image/20200816100042.png)

```bash
127.0.0.1:6379> set key1 "hello,zhangxl"
OK
127.0.0.1:6379> get key1
"hello,zhangxl"
127.0.0.1:6379> GETRANGE key1 0 3  截取字符串
"hell"
127.0.0.1:6379> GETRANGE key1 0 -1
"hello,zhangxl"
127.0.0.1:6379> 
```

![](https://photos.alitaalice.cn/image/20200816100459.png)

```bash
127.0.0.1:6379> SETEX key3 30 hello  #设置过期时间
OK
127.0.0.1:6379> ttl key3
(integer) 27
127.0.0.1:6379> ttl key3
(integer) 21
127.0.0.1:6379> SETNX mykey redis    #如果mykey不存在 创建mykey
(integer) 1
127.0.0.1:6379> keys *
1) "keys"
2) "key2"
3) "key1"
4) "mykey"
127.0.0.1:6379> SETNX mykey xx    #如果mykey存在 创建失败
(integer) 0
127.0.0.1:6379> get mykey
"redis"
127.0.0.1:6379> 
```

```bash
127.0.0.1:6379> MSET k1 v1 k2 v2 k3 v3
OK
127.0.0.1:6379> get keys *
(error) ERR wrong number of arguments for 'get' command
127.0.0.1:6379> keys *
1) "k1"
2) "k3"
3) "k2"
127.0.0.1:6379> mget k1 k2 k3  #同时获取多个值
1) "v1"
2) "v2"
3) "v3"
127.0.0.1:6379> msetnx k1 v1 k4 v4 #msetnx 是一个原子性的操作
(integer) 0
127.0.0.1:6379> get k4
(nil)
```

```bash
127.0.0.1:6379> getset db redis   #get and set操作
(nil)
127.0.0.1:6379> get db
"redis"
127.0.0.1:6379> getset db mongodb
"redis"
127.0.0.1:6379> get db
"mongodb"
```

String 类似的使用场景 

- value 
- 统计多单位的数量  
- 粉丝数
- 对象缓存存储