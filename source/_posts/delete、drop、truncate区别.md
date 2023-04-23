---
title: 'delete、drop、truncate区别'
date: 2020-06-03 14:56:16
tags: mysql
categories: mysql  
---

## 概述

> 本章介绍delete、drop、truncate区别

<!--more-->

## 正文

SQL关于删除的三个语句：**DROP**、**TRUNCATE**、 **DELETE** 的区别。

**DROP:**

```
DROP test;
```

删除表test，并释放空间，将test删除的一干二净。

**TRUNCATE:**

```
TRUNCATE test;
```

删除表test里的内容，并释放空间，但不删除表的定义，表的结构还在。

**DELETE:**

1、删除指定数据

删除表test中年龄等于30的且国家为US的数据

```
DELETE FROM test WHERE age=30 AND country='US';
```

2、删除整个表

仅删除表test内的所有内容，保留表的定义，不释放空间。

```
DELETE FROM test 或者 DELETE FROM test;
DELETE * FROM test 或者 DELETE * FROM test;
```