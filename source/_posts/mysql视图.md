---
title: mysql视图
date: 2020-05-09 22:42:36
tags: mysql
categories: mysql
---

## 概述

> 本章介绍视图究竟是什么，它们怎么样工作，何时使用它们。

<!--more-->

## 正文

视图是 虚拟的表，与包含数据的表不一样，视图只包含使用时动态检索数据的查询。

示例：

```
SELECT cust_name ,cust_contact FROM customers ,orders ,orderitems WHERE customers.cust_id=orders.cust_id  AND orderitems.order_num =orders.order_num
AND prod_id ='TNT2';
```

假设把整个查询包装成一个名叫productcustomers的虚拟表，则

```
SELECT cust_name,cust_contact FROM productcustomers WHERE prod_id='TNT2';
```

### 为什么使用视图

- 重用SQL 语句
- 简化复杂的SQL语句，在编写查询后，可以方便地重用它而不必知道它的基本查询细节。
- 使用表的组成部分而不是整个表
- 保护数据，可以给用户授予表的特定部分的访问权限，而不是整个表的访问权限。
- 更改数据格式和表示。

### 视图的规则和限制

- 视图必须唯一命名
- 对于创建的视图数目没有限制
- 视图可以嵌套
- 视图不能索引，不能有关联的触发器或者默认值

### 使用视图

- 视图用CREATE VIEW 来创建 
- 使用SHOW CREATE VIEW viewname; 来查看创建视图的语句
- 用DROP 来删除视图。语法为DROP VIEW viewname;
- 更新视图时，可以 先用DROP 再用CREATE  也可以直接使用CREATE OR REPLACE VIEW
- 可以先用DROP 再用 CREATE  也可以直接用CREATE OR REPLACE VIEW

### 利用视图简化复杂的联结

```c
CREATE VIEW productcustomers AS SELECT cust_name,cust_contact,prod_id
FROM customers,orders,orderitems WHERE customers.cust_id=orders.cust_id
AND orderitems.order_num =orders.order_name;
```

那么为了检索订购产品的TNT2客户

```C
SELECT cust_name,cust_contact FROM productcustomers WHERE prod_id ='TNT2';
```

### 使用视图重新格式化检索出的数据

下面的SELECT  语句在单个组合计算列中返回供应商名和位置

```c
SELECT Concat(RTrim(vend_name),'(',RTrim(vend_country),')') AS vend_title
FROM vendors
ORDER BY vend_name;
/*out 
    vend_title
    ACME  (USA)
    Jet Set (England)
    LT Supplies (USA)
 */
```

现在，假如经常需要这个格式的结果，不必在每次需要时执行联结，创建一个视图

```c
CREATE VIEW vendorlocations AS SELECT Concat(RTrim(vend_name),'(',RTrim(vend_country),')') AS vend_title
FROM vendors
ORDER BY vend_name;
```

now 

```
SELECT * FROM vendorlocations;
```

### 使用视图过滤不想要的数据

```
CREATE VIEW customeremaillist AS SELECT cust_id,cust_name,cust_email FROM customers WHERE cust_email IS NOT NULL;
```

在发送电子邮件到邮件列表时，需要排除没有电子邮件地址的用户

现在，可以像使用其他表一样使用视图customeremaillist 

```c
SELECT *
FROM customeremaillist;
```

### 使用视图与计算字段

```c
SELECT prod_id,
       quantity,
       item_price,
       quantity*item_price AS expanded_price
FROM orderitems
WHERE order_num =20005;
```

现在转换为视图

```
CREATE VIEW orderitemsexpanded AS 
SELECT order_num,
       prod_id,
       quantity,
       item_price,
       quantity*item_price AS expanded_price
FROM orderitems;
```

检索订单20005的详细内容

```
SELECT * FROM orderitemsexpanded WHERE order_num =20005;
```

### 更新视图

视图是可更新的，更新一个视图将更新其基表。如果你对视图增加或者删除行，实际上是对其基表增加或者删除行。

但是并非所有的视图都是可更新的

- 分组 （使用GROUP BY 和 HAVING )
- 联结
- 子查询
- 并
- 聚集函数 （Min() ,Count(),Sum() 等）；
- DISTINCT;  （用于返回不重复的值 ，select distinct name,id from A
- 导出（计算）列

