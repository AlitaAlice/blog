---
title: Redis_Set
date: 2020-08-19 10:20:03
tags: redis
categories: redis
---

## 概述

> 本章介绍Redis_Set

<!--more-->

## 正文

## Set(集合)

set中的值是不能重复的

```bash
127.0.0.1:6379> sadd myset hello  #set 添加元素
(integer) 1
127.0.0.1:6379> SADD myset world
(integer) 1
127.0.0.1:6379> SADD myset zhangxl
(integer) 1
127.0.0.1:6379> SMEMBERS myset  #查看set所有值
1) "world"
2) "hello"
3) "zhangxl"
127.0.0.1:6379> SISMEMBER myset hello  #判断元素是否在set中
(integer) 1
127.0.0.1:6379> SISMEMBER myset ll
(integer) 0
###########################
127.0.0.1:6379> SCARD myset #获取集合中的个数
(integer) 3
#################
127.0.0.1:6379> srem myset hello #移除set集合中的指定元素
(integer) 1
127.0.0.1:6379> SMEMBERS myset
1) "world"
2) "zhangxl"
#################################
set 无序不重复集合 
127.0.0.1:6379> SRANDMEMBER myset  #随机抽选出一个元素
"world"
#######################
删除指定的key  删除随机的key
127.0.0.1:6379> spop myset   #删除随机的key
"world"
127.0.0.1:6379> SRANDMEMBER myset
"zhangxl"
```

```bash
127.0.0.1:6379> sadd myset hello
(integer) 1
127.0.0.1:6379> sadd myset world
(integer) 1
127.0.0.1:6379> sadd myset zhangxl
(integer) 1
127.0.0.1:6379> sadd myset iloveu
(integer) 1
127.0.0.1:6379> sadd myset2 set2
(integer) 1
127.0.0.1:6379> SMOVE myset myset2 zhangxl #移动命令
(integer) 1
127.0.0.1:6379> SMEMBERS myset2
1) "zhangxl"
2) "set2"
```

```bash
127.0.0.1:6379> sadd key1 a
(integer) 1
127.0.0.1:6379> sadd key1 b
(integer) 1
127.0.0.1:6379> sadd key1 c
(integer) 1
127.0.0.1:6379> sadd key1 d
(integer) 1
127.0.0.1:6379> sadd key2 d
(integer) 1
127.0.0.1:6379> sadd key2 e
(integer) 1
127.0.0.1:6379> sadd key2 f
(integer) 1
127.0.0.1:6379> sdiff key1 key2  #差集
1) "a"
2) "b"
3) "c"
127.0.0.1:6379> SUNION key1 key2   #并集
1) "d"
2) "a"
3) "f"
4) "e"
5) "c"
6) "b"
127.0.0.1:6379> sinter key1 key2  #交集
1) "d"
```

## Hash (哈希)

Map集合 key-value

```bash
127.0.0.1:6379> hset myhash m1 v1    # key-value
(integer) 1
127.0.0.1:6379> hset myhash m2 v2
(integer) 1
127.0.0.1:6379> hset myhash m3 v3
(integer) 1
127.0.0.1:6379> hmset myhash m4 v4 m5 v5    #批量设置
OK
127.0.0.1:6379> hmget myhash m1 m2 m3 m4 m5
1) "v1"
2) "v2"
3) "v3"
4) "v4"
5) "v5"
127.0.0.1:6379> hgetall myhash   #获取所有
 1) "m1"
 2) "v1"
 3) "m2"
 4) "v2"
 5) "m3"
 6) "v3"
 7) "m4"
 8) "v4"
 9) "m5"
10) "v5"
127.0.0.1:6379> hdel myhash m1   #删除某个key  and value
(integer) 1
127.0.0.1:6379> hgetall myhash
1) "m2"
2) "v2"
3) "m3"
4) "v3"
5) "m4"
6) "v4"
7) "m5"
8) "v5"
```

```bash
127.0.0.1:6379> hgetall myhash
1) "m2"
2) "v2"
3) "m3"
4) "v3"
5) "m4"
6) "v4"
7) "m5"
8) "v5"
127.0.0.1:6379> hlen myhash   #判断hash长度
(integer) 4
127.0.0.1:6379> hexists myhash m2  #判断某一field是否存在
(integer) 1
127.0.0.1:6379> hexists myhash m6
(integer) 0
```

```bash
127.0.0.1:6379> hkeys myhash    #获得所有keys
1) "m2"
2) "m3"
3) "m4"
4) "m5"
127.0.0.1:6379> hvals myhash   #获得所有vals
1) "v2"
2) "v3"
3) "v4"
4) "v5"
```

```bash
127.0.0.1:6379> hincrby myhash field1 1   #指定增量
(integer) 6
127.0.0.1:6379> hget myhash field1
"6"
127.0.0.1:6379> hincrby myhash field1 1
(integer) 7
127.0.0.1:6379> hget myhash field1
"7"
127.0.0.1:6379> hsetnx myhash field1 hello
(integer) 0
127.0.0.1:6379> hsetnx myhash field1 h111
(integer) 0
127.0.0.1:6379> hgetall myhash
 1) "m2"
 2) "v2"
 3) "m3"
 4) "v3"
 5) "m4"
 6) "v4"
 7) "m5"
 8) "v5"
 9) "field1"
10) "7"
127.0.0.1:6379> hsetnx myhash ssdsa 111   #如果不存在则可以设置，如果存在不可以设置
(integer) 1
127.0.0.1:6379> hgetall myhash
 1) "m2"
 2) "v2"
 3) "m3"
 4) "v3"
 5) "m4"
 6) "v4"
 7) "m5"
 8) "v5"
 9) "field1"
10) "7"
11) "ssdsa"
12) "111"
```

## Zset(有序集合)

在set的基础上，增加了一个值

  set k1      v1 

  zset  k1    score v1 

```bash
127.0.0.1:6379> zadd myset 1 one 2 two 3 three  # score value
(integer) 3
127.0.0.1:6379> ZRANGE myset 0 -1
1) "one"
2) "two"
3) "three"
```

