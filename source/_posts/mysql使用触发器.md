---
title: mysql使用触发器
date: 2020-05-15 15:38:16
tags: mysql
categories: mysql
---

## 概述

> 本章介绍触发器

<!--more-->

## 正文

触发器是MySQL响应以下任意语句而自动执行的一条MySQL语句（或位于BEGIN和END语句之间的一组语句 。

- DELETE 

- INSERT 

- UPDATE

  在创建触发器时，需要给出4条信息 :

  ![](https://photos.alitaalice.cn/image/20200515154008.png)

Eg：

```java
CREATE TRIGGER newproduct AFTER INSERT ON products
FOR EACH ROW SELECT 'Product added'
```

CREATE TRIGGER用来创建名为newproduct的新触发器。触发器
可在一个操作发生之前或之后执行，这里给出了AFTER INSERT，
所以此触发器将在INSERT语句成功执行后执行。这个触发器还指定FOR EACH ROW，因此代码对每个插入行执行。在这个例子中，文本Product added将对每个插入的行显示一次.

  每个表最多支持6个触发器（每条INSERT、 UPDATE和DELETE的之前和之后）。单一触发器不能与多个事件或多个表关联，所以，如果你需要一个对INSERT和UPDATE操作执行的触发器，则应该定义两个触发器  .

## 删除触发器

```
DROP TRIGGER newproduct;
```

触发器不能更新或覆盖。为了修改一个触发器，必须先删除它，然后再重新创建。  

## 使用 触发器

### 1 INSERT 触发器

INSERT触发器在INSERT语句执行之前或之后执行。  

- 在INSERT触发器代码内，可引用一个名为NEW的虚拟表，访问被插入的行；
- 在BEFORE INSERT触发器中， NEW中的值也可以被更新（允许更改被插入的值）；
-  对于AUTO_INCREMENT列， NEW在INSERT执行之前包含0，在INSERT 执行之后包含新的自动生成值  

eg：

```java
CREATE TRIGGER neworder AFTER INSERT ON orders
FOR EACH ROW SELECT NEW.order_num;
```

此代码创建一个名为neworder的触发器，它按照AFTER INSERT
ON orders执行。在插入一个新订单到orders表时， MySQL生
成一个新订单号并保存到order_num中。触发器从NEW. order_num取得这个值并返回它。此触发器必须按照AFTER INSERT执行，因为在BEFORE INSERT语句执行之前，新order_num还没有生成。对于orders的每次插入使用这个触发器将总是返回新的订单号。  

试着插入一下新行：

```
INSERT INTO orders(order_date,cust_id) VALUES(NOW(),10001);
```

![](https://photos.alitaalice.cn/image/20200515155708.png)

### DELETE 触发器

-  在DELETE触发器代码内，你可以引用一个名为OLD的虚拟表，访问被删除的行；
- OLD中的值全都是只读的，不能更新。  

下面例子用OLD保存将要被删除的行到一个存档表中

```java
CREATE TRIGGER deleteorder BEFORE DELETE ON orders
FOR EACH ROW
BEGIN
    INSERT INTO archive_orders(order_num, order_date,cust_id) VALUES(OLD.order_num,OLD.order_date,OLD.cust_id);
END;
```

在任意订单被删除前将执行此触发器。它使用一条INSERT语句将OLD中的值（要被删除的订单）保存到一个名为archive_orders的存档表中（为实际使用这个例子，你需要用与orders相同的列创建一个名为archive_orders的表）  

## UPDATE 触发器

- 在UPDATE触发器代码中，你可以引用一个名为OLD的虚拟表访问以前（UPDATE语句前）的值，引用一个名为NEW的虚拟表访问新更新的值；
- 在BEFORE UPDATE触发器中， NEW中的值可能也被更新（允许更改将要用于UPDATE语句中的值）；

-  OLD中的值全都是只读的，不能更新  

```java
CREATE TRIGGER updatevendor BERORE UPDATE ON vendors
FOR EACH ROW SET NEW.vend_state=Upper(NEW.vend_state);
```

