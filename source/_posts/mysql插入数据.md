---
title: mysql插入数据
date: 2020-05-07 22:54:46
tags: mysql
categories: 后端
---

## 概述

> 本章介绍如何利用SQL的INSERT语句将数据插入到表中

<!--more-->

## 正文

## 插入到完整的行

```c
INSERT INTO Customers
VALUES(NULL,
       'PEP E.LAPEW',
       '100 MAIN STREET',
        'Los Angeles',
         'CA',
        '90046',
         'USA',
          NULL,
          NULL);
```

编写INSERT语句的更加安全（不过更加繁琐）

```
INSERT INTO customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contact,cust_email)
VALUSES('PEP E.LAPEW',
       '100 MAIN STREET',
        'Los Angeles',
         'CA',
        '90046',
         'USA',
          NULL,
          NULL');
```

### 省略列

- 该列定义为允许null值
- 在表定义中给出默认值

### 提高整体性能

如果数据检索是最重要的，那你可以通过在INSERT INTO 之间添加关键字

LOW_PRIORITY 指示Mysql降低INSERT语句的优先级

```
INSERT LOW_PRIORITY INTO
```

## 插入多个行

```c
INSERT INTO customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contact,cust_email)
VALUSES('PEP E.LAPEW',
       '100 MAIN STREET',
        'Los Angeles',
         'CA',
        '90046',
         'USA',
          NULL,
          NULL'),
       ('PEP E.LAPEW',
       '100 MAIN STREET',
        'Los Angeles',
         'CA',
        '90046',
         'USA',
          NULL,
          NULL');
```

其中单条INSERT语句有多组值，每组值用一对圆括号括起来，用逗号分隔。

### 插入检索出的数据

```c
INSERT INTO customers(cust_id,cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contact,cust_email)
SELECT cust_id,cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contact,cust_email FROM custnew;
```

这个例子中INSERT SELECT 从custnew中将所有数据导入到customer中。

**其实MYSQL不关心SELECT返回的列名，它使用的是列的位置，因此SELECT中的第一列用来填充表列中指定的第一列**。