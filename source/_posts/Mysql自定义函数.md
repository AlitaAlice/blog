---
title: Mysql自定义函数
date: 2020-05-18 22:08:27
tags: mysql
categories: mysql
---

## 概述

> 本章介绍Mysql自定义函数

<!--more-->

## 正文

创建函数语法：
CREATE FUNCTION fn_name(func_parameter[,...])
RETURNS type
[characteristic...]
routine_body

eg:

```java
#创建一个函数
DELIMITER $$ -- 定界符
-- 开始创建函数
CREATE FUNCTION user_main_fn(v_id INT)
RETURNS VARCHAR(50)
BEGIN
  -- 定义变量
  DECLARE v_userName VARCHAR(50);
  -- 给定义的变量赋值
  SELECT f_userName INTO v_userName FROM t_user_main 
  WHERE f_userId = v_id;
  -- 返回函数处理结果
  RETURN v_userName;
END $$ -- 函数创建定界符
DELIMITER; 
```

```java
#创建第二个函数，使用第一个函数
DELIMITER $$
CREATE FUNCTION user_main_fn2(v_id INT)
RETURNS VARCHAR(100)
BEGIN 
  #定义变量
  DECLARE v_userName VARCHAR(50);
  DECLARE  v_userNameNew VARCHAR(50);
  #通过into赋值
  SELECT f_userName INTO v_userName FROM t_user_main WHERE f_userId = v_id;
  #使用函数
  SELECT user_main_fn(v_id) INTO v_userNameNew FROM DUAL;
  #返回函数处理结果
  RETURN CONCAT(v_userName,'***',v_userNameNew);
END $$
DELIMITER;
```

DUAL 虚拟表

### 查看函数状态语法：

```java
SHOW FUNCTION STATUS [LIKE 'pattern']
```



#### 查看函数的定义语法：

```java
SHOW CREATE FUNCTION fn_name;
```

eg:  输出第n高的工资

```java
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N=N-1;
  RETURN (
      # Write your MySQL query statement below.
      SELECT  DISTINCT Salary  FROM Employee ORDER BY Salary DESC  limit N,1
  );
END
```

