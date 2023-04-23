---
title: mysql更新和删除数据
date: 2020-05-07 23:12:09
tags: mysql
categories: 后端
---

## 概述

> 本章介绍如何利用UPDATA和DELETE语句进一步操控表数据

<!--more-->

## 正文

## 更新数据

- 更新特定行
- 更新所有行 **特别注意不要省略WHERE子句 稍不注意就会更新表中的所有行**

```c
UPDATA customers SET cust_email ='elmer@gmail.com' WHERE cust_id =10005;
```

更新多个列： 用逗号分隔

```c
UPDATE customers SET cust_name='The Fudds',
cust_email='elmer@gmail.com'
WHERE cust_id =10005;
```

### IGNORE关键字

如果用UPDATE 语句更新多行，并且在更新这些行中的一行或多行时出现一个现错误，则整个UPDATE操作被取消。

为即使是发生错误，也继续进行更新可以使用**IGNORE**关键字

```c
UPDATE IGNORE customers...
```

## 删除数据

- 从表中删除特定的行
- 从表中删除所有行  **不要省略WHERE子句**

```c
DELETE FROM customers WHERE cust_id =10006;
```

### 更快的删除

如果想删除所有行

```
TRUNCATE TABLE
```

