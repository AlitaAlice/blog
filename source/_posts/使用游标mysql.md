---
title: 使用游标mysql
date: 2020-05-14 17:32:39
tags: mysql
categories: mysql
---

## 概述

> 本章介绍游标

<!--more-->

## 正文

 MySQL检索操作返回一组称为结果集的行。这组返回的行都是与SQL语句相匹配的行（零行或多行）。使用简单的SELECT语
句，例如，没有办法得到第一行、下一行或前10行，也不存在每次一行地处理所有行的简单方法（相对于成批地处理它们）  

游标（cursor） 是一个存储在MySQL服务器上的数据库查询，
它不是一条SELECT语句，而是被该语句检索出来的结果集。在存储了游标之后，应用程序可以根据需要滚动或浏览其中的数据.  

只能用于存储过程 不像多数DBMS， MySQL游标只能用于
存储过程（和函数）  

## 1 创建游标

```
CREATE PROCEDURE processorders()
BEGIN 
   DECLARE ordernumbers CURSOR
   FOR
   SELECT order_num FROM orders
END;
```

DECLARE语句用来定义和命名游标，这里为ordernumbers。 存储过程处理完成后，游标就消失（因为它局限于存储过程）  

## 2 打开和关闭游标  

输入：

```java
 OPEN ordernumbers;
```

```java
关闭游标： CLOSE ordernumbers;
```

如果你不明确关闭游标，MySQL将会在到达END语句时自动关闭它。

前面的例子修改版本：

```java
CREATE PROCEDURE processorders()
BEGIN
     --Declare the cursor
     DECLARE ordernumbers CURSOR
     FOR
     SELECT order_num FROM orders;
     --Open the cursor
     OPEN ordernumbers;
     --Close the cursor
     CLOSE ordernumbers;
     
     END;
```

声明打开和关闭一个游标。

```java
CREATE PROCEDURE processorders()
BEGIN
    --Delare local variables
    DECLARE done BOOLEAN DEFAULT 0;
    DECLARE o INT;
    --Declare the cursor
    DECLARE ordernumbers CURSOR
    FOR
    SELECT order_num FROM orders;
    --Declare continue handler
    DELARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done=1;
    --Open the cursor
    OPEN ordernumbers;
    --LOOP through all rows
    REPEAT
    
    --GET order number
    FETCH ordernumbers INTO o;
    --End of loop
    UNTIL done END REPEAT;
    --Close the cursor
    CLOSE ordernumbers;
    END;
    
```

FETCH是在REPEAT内，因此它反复执行直到done为真（由UNTIL
done END REPEAT;规定）。为使它起作用，用一个DEFAULT 0（假，不结束）定义变量done。那么， done怎样才能在结束时被设置为真呢？答案是用以下语句：  

```java
DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done=1;
```

这条语句定义了一个CONTINUE HANDLER，它是在条件出现时被执行的代码。这里， 它指出当SQLSTATE '02000'出现时， SET done=1。SQLSTATE'02000'是一个未找到条件， 当REPEAT由于没有更多的行供循环而不能继续时，出现这个条件。  