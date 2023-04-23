---
title: mysql必知必会
date: 2020-05-03 09:59:42
tags: mysql
categories: mysql
---
## 1 基础操作

 登录mysql -u root -p
 Show databases;
 Use databasename;
Show tables;  //显示行
<!--more-->
 Show columns from xxx;   //显示列 

## 第一章

SELECT DISTINCT  published FROM t_blog ;  DISTINCT此关键字指示只返回不同的值。 
 SELECT id FROM t_blog LIMIT 5;
 SELECT id FROM t_blog LIMIT 3,3; //从第三行开始的后三行
 SELECT t_blog.id FROM blog.t_blog;   完全限定的列名和表名 和之前的用法一样。
 SELECT id,type_id,user_id FROM t_blog ORDER BY type_id,id;  先对type_id排序 再对id进行排序。
 DESC 降序 ASC 升序  默认升序
 SELECT id FROM t_blog ORDER BY type_id LIMIT 1; 此种方式找到了数值最大的一行。
 **在使用where 过滤时 ，order by 排序要在where的后面**
 SELECT id FROM t_blog  where id <>10;   <> 不匹配检查
 范围值检查
  SELECT ID FROM T_BLOG WHERE ID BETWEEN 10 AND 20 :
 Select id from t_blog where id is null;  空值检查
 Select id,user_id from t_blog where id <=10 and user_id <=1;
 Select prod_name,prod_price from products where vend_id=1002 or vend_id =1003 and 
  Prod_price>=10; SQL处理OR操作符和AND操作符时，优先处理AND操作符。
 故先处理 vend_id =1003 and prod_price>=10  或者  vend_id=1002  ；
解决方法是 
Select prod_name,prod_price from products where (vend_id =1002 or vend_id =1003) and prod_price >=10    用( )来明确分组操作符。DBMS 首先过滤圆括号内的OR条件。
NOT 在MYSQL中的NOT中 MYSQL支持使用NOT 对IN,BETWEEN 和EXISTS子句取反。这与多数其他DBMS允许使用NOT对各种条件取反有很大区别。
######
通配符
用来匹配值的一部分的特殊字符
LIKE 指示MYSQL 后跟的搜索模式利用通配符匹配而不是直接相等匹配比较
SELECT prod_name FROM products WHERE prod_name REGEXP ‘[123] Ton’
ORDER BY prod_name;
正则表达式 [123]Ton 其中[123]定义一组字符 
它的意思是匹配1或2或3  因此 1ton 和2ton 都匹配且返回了
[] 其实是另一种形式的OR语句 
[1|2|3]Ton 的缩写 为 [123]Ton  
1|2|3 Ton 的意思是检索出1或2或3 ton 
[^123] 匹配除这些字符除外的任何东西	
 ^ 是REGEXP的否定符号
在匹配范围中
0到9  将由[0123456789] 等同于 [0-9]
.表示匹配一个字符
输入 SELECT vend_name FROM vendors WHERE vend_name REGEXP ‘.’ ORDER BY vend_name
.匹配任意字符  这时每一行都被检索出来 为了匹配特殊字符 必须用\\ 作为前导
如
SELECT vend_name FROM vendors WHERE vend_name REGEXP ‘\\.’ ORDER BY vend_name
这才是期望的输出 \\.匹配. 这种处理就是所谓的转义。
？ 字符 ？匹配它前面的任何字符的0次或者1次出现。
 如 SELECT prod_name FROM products WHERE prod_name REGEXP ‘\\([0-9] sticks?\\)’
 ORDER BY prod_name ;
Sticks 匹配 stick 和sticks s后的?使s可选 
另外例如 
SELECT prod_name FROM products WHERE prod_name REGEXP ‘[[:digit:]]{4} 
ORDER BY prod_name；
[:digit:]匹配任意数字
因而它作为数字的一个集合
{4} 确切的要求它前面的字符 出现4次
匹配特定位置的文本，需要使用表9-4列出的定位符
^ 文本的开始
$ 文本的结尾
[[:<:]] 词的开始
[[:>;]] 词的结尾
‘^[0-9\\.]’ 找出一个数 包括以小数点开始的数开始的所有产品。
SELECT prod_name FROM products WHERE prod_name REGEXP ‘^[0-9\\.]’
ORDER BY prod_name;

## 第10章  创建计算字段 

MySQL 使用Concat() 函数来实现
SELECT Concat(vend_name,’（‘，vend_country,’）’)
FROM vendors ORDER BY vend_name;
拼接  将值联结到一起构成单个值
比如以上的输出为 
ACME (USA)
删除数据右侧多余的空格来整理数据
MySQL 的RTrim()可以去掉值右边的所有的空格
SELECT Concat(RTrim(vend_name),’(‘,RTrim(vend_country),’)’)
FROM vendors 
ORDER BY vend_name;
LTrim() 去掉串左边的空格
Trim()去掉左右俩边的空格
SELECT Concat (RTrim(vend_name),’(‘,RTrim(vend_country),’)’)AS vend_title FROM vendors ORDER BY vend_name;
一个未命名的列不能用于客户机的应用中，因为客户机没有办法去引用它。
所以才出现了别名。AS 关键字来赋予别名 任何客户机应用都可以按名来引用这个列，就像它是一个实际的表列一样。



执行算数运算
SELECT pro_id,quantity,item_price FROM oderitems WHERE order order_num =20005;
在算数运算中 检索200005中的所有物品
如果要计算汇总物品的价格
SELECT prod_id ,quantity,item_price, quantity*item_price  AS expanded_price FROM oderitems WHERE order_num =20005;
此时客户机可以使用这个新计算的列，就像其他列一样。
MYSQL 支持基本算术运算符



## 第十一章 使用数据来处理函数

SELECT vend_name,Upper(vend_name) AS  vend_name_upcase FROM vendors ORDER BY vend_name;
Upper()将文本转换为大写 
常用的文本处理函数：
Left() 返回串左边的字符
Length() 返回串的长度
Locate()返回串的一个子串
Lower()将串转换为小写
LTrim() 去掉左边的空格
Right()返回串右边的字符
RTrim() 去掉串右边的空格
Soundex()返回串的Soundex值
SubString() 返回子串的字符
Upper() 大写
Soundex（） 将任何文本串转换为描述其语音表示的字母数字模式的算法
如
SELECT cust_name ,cust_contact FROM customers WHERE cust_contact =’Y.Lie’;
其联系名是为Y.Lee 此时没办法搜索到
但是通过
SELECT cust_name,cust_contact FROM customers WHERE Soundex(cust_contact)=Soundex(‘Y.lie);
此时可以搜索到Y.Lee
日期和时间的处理函数
Date() 返回日期部分的日期部分
Year() 返回日期部分的年份部分
Day()
Month()

如：
SELECT cust_id,oder_num FROM oders WHERE Date(order_date)=’2005-09-01’;
SELECT cust_id,order_num FROM orders WHERE Date(order_date) BETWEEN ‘2005-09-01’AND’2005-03-30’;
数值处理函数
Abs() 返回数的绝对值

Cos() 角度的余弦
Exp() 返回一个数的指数值
Mod() 操作数的余数
……

## 第12章 汇总数据

12.1 聚集函数  运行在行组上，计算和返回单个值得函数
AVG() 返回某列的平均值
COUNT()  返回某列的行数
MAX() 返回某列的最大值
MIN() 返回某列的最小值
SUM() 返回某列值之和 
SELECT AVG(prod_price) AS avg_price FROM products;\
AVG() 也可以用来确定列或行当平均值
SELECT AVG(prod_price) AS avg_price FROM products WHERE vend_id =1003;
COUNT () 函数
COUNT(*)对表中的行的数目进行技术
COUNT(column) 对特定列中具有值的行进行计数
例如SELECT COUNT(*) AS num_cust FROM customers;
利用COUNT(*)对所有行计数
SELECT COUNT(cust_email) AS num_cust FROM customers;
对于cust_email中所有有值的行进行计数
MAX() 指定列中的最大值 MAX()要求指定列名。
MIN() 
SUM() 也可以用来合计计算值 用来得出总的订单金额
SELECT SUM(item_price  *quantity) AS total_price FROM oderitems WHERE order_num=20005;
SUM(item_price *quantity) 返回订单中所有物品价钱之和

## 第13章 分组数据

```
SELECT vend_id ,COUNT(*) AS num_prods FROM products GROUP BY vend_id;
```

Vend_id num_prods
1001        3
1002        2
1003        7
1005        2
上述语句将vend_id进行分组，GROUP BY 对于分组的整个结果集进行聚集
使用ROLLUP 使用WITH ROLLUP 关键字，将得到每个分组以及分组汇总级别的值
2如何过滤分组?
HAVING
如： SELECT cust_id ,COUNT(*)AS orders FROM orders GROUP BY cust_id 
HAVING COUNT(*) >=2
它过滤COUNT(*)>=2 的那些分组
输入： SELECT vend_id,COUNT(*) AS num_prods FROM products WHERE prod_price >=10
GROUP BY vend_id HAVING COUNT(*)>=2;
13.4 分组和排序
GROUP BY 和ORDER BY 
GROUP BY  是在ORDER BY 之前，在where 之后

# group by 和 order by 的区别 + 理解过程

https://blog.csdn.net/sinat_40692412/article/details/81200133

## 第14章 子查询

子查询：嵌套在其他查询中的查询
1 检索包含物品TNT2 的所有订单的编号
 SELECT order_num FROM orderitems WHERE prod_id =’TNT2’；
2 检索具有前一步骤列出的订单编号的所有客户的ID
 SELECT cust_id FROM orders WHERE order_num IN (20005,20007);
3 现在把第一个查询变为子查询 组合成俩个查询：
 SELECT cust_id FROM oders WHERE order_num IN (SELECT order_num FROM orderitems WHERE prod_id =’TNT2’);
在SELECT 语句中，子查询总是从内向外查询处理。
检索这些客户的ID的客户信息，检索俩列的SQL语句为：
SELECT cust_name, cust_contact FROM customers WHERE cust_id IN (10001,10004);
则可以转换为：
SELECT cust_name ,cust_contact FROM customers WHERE cust_id IN (SELECT cust_id FROM orders WHERE order_num IN (SELECT order_num FROM orderitems WHERE prod_Id =’TNT2’))；
计算结果子查询：
SELECT cust_name,cust_state,(SELECT COUNT(*) FROM oders WHERE orders.cust_id=customers.cust_id)AS orders FROM customers ORDER BY cust_name;

## 第15 章  联结表  join 表

外键位某个表中的一列 它包含另一个表的主键值定义了俩个表之间的关系。

```
SELECT vent_name,prod_name,prod_price 
FROM vendors ,products 
WHERE vendors.vend_id=products.vend_id;
ORDER BY vend_name,prod_name ;  
```

此种方法通过WHERE子句来限定了列名 ，如果要给出 vend_id 那么mysql_id 并不知道是哪个
存在一种状况是 
笛卡尔积：
在不指定where子句时

```
SELECT vend_name ,prod_name,prod_price 
FROM vendors,products ORDER BY vend_name,prod_name;
```

### 15.2.2 内部联结

目前为止所使用的联结称为 等值联结  它基于俩个表之间的相等测试 这种联结也叫内部联结。

```
SELECT vend_name , prod_name , prod_price FROM vendors INNER JOIN products ON vendors.vend_id =products.vend_id ;
```

此时使用的是INNER JOIN  联结条件用的是ON

### 联结多个表：

```
SELECT prod_name,vend_name,prod_price,quantity FROM orderitems,products,vendors WHERE products.vend_id =vendors.vend_id AND orderitems.prod_id =products.prod_id AND order_num =20005;
```



## 第16章 创建高级联结

### 使用表别名

SELECT Concat(RTrim(vend_name)，‘（’，RTrim（vend_country）,’）’) AS vend_title FROM vendors ORDER BY vend_name;

### 内部联结：

它基于俩个表之间的相等测试
SELECT vend_name .prod_name,prod_price FROM vendors INNER JOIN products ON vendors.vend_id =produces.vend_id;

### 自联结： 引用别名，自己联结自己

SELECT p1.prod_id,p1.prod_name FROM products AS p1,products AS p2
WHERE p1.vend_id =p2.vend_id AND p2.prod_id =’DTNTR’;
此查询种需要的俩个表实际上是相同的表。
因此products 表在from 子句中出现了俩次。虽然这是合法的，但是对products 的引用具有二义性。因此使用了别名。（用自联结而不用子查询。有时候处理联结要比处理查询要快的多）

### 自然联结：

其中你只能选择那些唯一的列。
通过对表使用通配符（SELECT *）对所有其他表的列使用明确的子集来完成的。*

```
SELECT c.*,o.ordr_num,o.order_date,oi.prod_id,oi.quantity,OI.item_price FROM customers AS c,orders AS o,orderitems AS oi WHERE c.cust_id =o.cust_id AND oi.order_num =o.order_num
AND prod_id =’FB’;
```


通配符只对第一个表使用，所有其他列明确列出，所以没有重复的列被检索出来。

### 外部联结：

许多联结将一个表中的行与另外一个表中的行相关联，但有时候会需要包含没有关联行的那些行，例如  可能需要使用联结来完成以下的工作：
1对每个客户下了多少订单进行计数，包括那些至今未下订单的客户。
2列出所有产品以及订购数量，包括没有人订购的产品
3计算平均销售规模，包括那些至今未下订单的客户
联结包含了那些在相关表中没有关联行的行，这种叫做外部联结	
内部联结检索所有客户及其订单：

```
SELECT customers.cust_id,order.orders.order_num FROM customers INNER JOIN orders ON
Customers.cust_id =orders.cust_id;
```

### 外部联结：

```
SELECT customers.cust_id ,orders.order_num FROM customers LEFT OUTER JOIN oders 
ON customers.cust_id =orders.cust_id;
```

输出为：

```
 cust_id   order_num
  10001      20005
  10001      20009
  10002       null
 10003       null
```

此时必须要用RIGHT 或LEFT 关键字指定包括其所有行的表 
其实就是左外部联结和右外部联结

此时必须要用RIGHT 或LEFT 关键字指定包括其所有行的表 
其实就是左外部联结和右外部联结

### 16.3 使用带聚集函数的联结

使用了COUNT（）函数的联结
SELECT customers.cust_name, customers.cust_id,COUNT(orders.order_num) AS num_ord FROM customers INNER JOIN orders ON customers.cust_id =orders.cust_id GROUP BY customers.cust_id;
SELECT 语句使用INNER JOIN 将customers和orders 表互相关联。 GROUP BY 子句按客户分组数据。
聚集函数也可以方便地与其他联结一起使用，
如 SELECT customers,cust_name,cusomers,cust_id,COUNT(orders,order_num)AS num_ord FROM customers LEFT OUTER JOIN orders ON customers.cust_id =orders.cust_id  GROUP BY customers.cust_id;

## 17 章 组合查询

利用UNION 操作符将多条SELECT 语句组合成一个结果集
执行多个查询，多个SELECT 语句 并将结果作为单个查询结果集返回。
这种称为并（union）或复合查询 
使用UNION
输入
SELECT vend_id ,prod_id ,prod_price FROM products WHERE prod_price <=5 
UNION
SELECT vend_id,prod_id,prod_price FROM products WHERE vend_id IN(1001,1002);
也可以使用多个where
SELECT vend_id ,prod_id,prod_price FROM products WHERE prod_price <=5 OR vend_id IN
(1001,1002); 
从多个表中检索数据的情形，使用UNION 可能会处理更简单。
17.2.2 UNION 规则
 1   UNION 的每个查询必须包含相同的列，表达式，或聚集函数

 2   UNION 的默认行为，如果想返回所有匹配行 可以使用UNION ALL 而不是UNION
 17.2.4 对组合查询结果排序
SELECT vend_id ,prod_id,prod_price FROM products WHERE prod_price <=5 
UNION 
SELECT vend_id,prod_id,prod_price FROM products WHERE vend_id IN (1001,1002)
ORDER BY vend_id ,prod_price ;

## 18章 全文本搜素

18.1 理解全文本搜素