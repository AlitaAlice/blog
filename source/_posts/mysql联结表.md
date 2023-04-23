---
title: mysql联结表
date: 2020-05-08 11:01:05
tags: mysql
categories: 后端
---

## 概述

> 本章介绍联结以及高级联结。

<!--more-->

## 正文

## 创建联结

```c
SELECT vent_name,prod_name,prod_price 
FROM vendors ,products 
WHERE vendors.vend_id=products.vend_id;
ORDER BY vend_name,prod_name ;  
```

## 内部联结

```c
SELECT vend_name , prod_name , prod_price FROM vendors INNER JOIN products ON vendors.vend_id =products.vend_id ;
```

此时使用的是INNER JOIN 联结条件用的是ON

联结多个表：

```c
SELECT prod_name,vend_name,prod_price,quantity FROM orderitems,products,vendors WHERE products.vend_id =vendors.vend_id AND orderitems.prod_id =products.prod_id AND order_num =20005;
```

## 创建高级联结

### 使用表别名

```c
SELECT Concat(RTrim(vend_name)，‘（’，RTrim（vend_country）,’）’) AS vend_title FROM vendors ORDER BY vend_name;
```

### 内部联结：

它基于俩个表之间的相等测试

```c
SELECT vend_name .prod_name,prod_price FROM vendors INNER JOIN products ON vendors.vend_id =produces.vend_id;
```

### 自联结： 引用别名，自己联结自己

假如你发现某物品（其ID为DTNRT)存在问题，因此想知道生产该物品的供应商生产的其他物品是否也存在这些问题。

```c
SELECT p1.prod_id,p1.prod_name FROM products AS p1,products AS p2
WHERE p1.vend_id =p2.vend_id AND p2.prod_id =’DTNTR’;
```

因此products 表在from 子句中出现了俩次。虽然这是合法的，但是对products 的引用具有二义性。因此使用了别名。（用自联结而不用子查询。有时候处理联结要比处理查询要快的多）

### 自然联结

**自然联结的意思是排除多次出现，使每个列只返回一次。**

**我们建立的每个内部联结都是自然联结。**

示例通过对表使用通配符（SELECT *）对所有其他表的列使用明确的子集来完成的。

```c
SELECT c.*,o.ordr_num,o.order_date,oi.prod_id,oi.quantity,OI.item_price FROM customers AS c,orders AS o,orderitems AS oi WHERE c.cust_id =o.cust_id AND oi.order_num =o.order_num
AND prod_id =’FB’;
```

通配符只对第一个表使用，所有其他列明确列出，但没有重复的列被检索出来。

### 外部联结：

**许多联结将一个表中的行与另外一个表中的行相关联，但有时候会需要包含没有关联行的那些行，**例如 可能需要使用联结来完成以下的工作：

- 对每个客户下了多少订单进行计数，包括那些至今未下订单的客户。
- 列出所有产品以及订购数量，包括没有人订购的产品
- 计算平均销售规模，包括那些至今未下订单的客户

**联结包含了那些在相关表中没有关联行的行，这种叫做外部联结**     

内部联结检索所有客户及其订单：

```
SELECT customers.cust_id,order.orders.order_num FROM customers INNER JOIN orders ON
Customers.cust_id =orders.cust_id;
```

外部联结：

```c
SELECT customers.cust_id ,orders.order_num FROM customers LEFT OUTER JOIN oders 
ON customers.cust_id =orders.cust_id;
```

输出为

```
 cust_id   order_num
  10001      20005
  10001      20009
  10002       null
  10003       null
```

此时必须要用RIGHT 或LEFT 关键字指定包括其所有行的表，如果是**LEFT**，就**指出包括OUTER JOIN左边表的所有行**。示例是包括（customers)表种所有行。

其实就是左外部联结和右外部联结

### 使用带聚集函数的联结

使用了COUNT（）函数的联结

```
SELECT customers.cust_name, customers.cust_id,COUNT(orders.order_num) AS num_ord FROM customers INNER JOIN orders ON customers.cust_id =orders.cust_id GROUP BY customers.cust_id;
```

```
SELECT customers,cust_name,cusomers,cust_id,COUNT(orders,order_num)AS num_ord FROM customers LEFT OUTER JOIN orders ON customers.cust_id =orders.cust_id  GROUP BY customers.cust_id;
```