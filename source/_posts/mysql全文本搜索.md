---
title: mysql全文本搜索
date: 2020-05-07 22:31:33
tags: mysql
categories: 后端
---

## 概述

> Mysql 全文本搜索用法实例及详解。

<!--more-->

## 正文

# 启用全文本搜索支持

CREATE  TABLE 接受FULLTEXT子句

```c
CREATE TABLE productsnotes
(
 note_id int NOT NULL AUTO_INCREMENT,  /* auto increment 自动递增主键字段 */
 prod_id char(10)  NOT NULL,
 note_date datetime NOT NULL,
 note_text  text  NULL,
 PRIMARY KEY(note_id),
 FULLTEXT(note_text)
 ) ENGINE=MyISAM;
```

这条CREATE TABLE 语句定义表productnotes 并列出它所包含的列即可。这些列中有一个名为note_text 的列，为了进行全文本搜素，MySQL根据子句FULLTEXT(note_text)的指示对它进行索引。
FULLTEXT索引单个列，如果需要也可以指定多个列。

## 在索引之后，使用俩个函数Match() 和Against()执行全文本搜素

其中Match()指定被搜索的列，Against()指定要使用的搜索表达式

```c
SELECT note_text FROM productnotes WHERE Match(not_text) Against('rabbit');
```

Match(note_text )指示MySQL针对指定的列进行搜索，Against('rabbit') 指定词rabbit作为搜索文本。

使用完整的Match()说明，传递给Match()的值必须与FULLTEXT()定义中的相同。除非使用BINARY 方式，否则全文本搜索不区分大小写。

- 搜索页可以简单地用LIKE子句完成


```c
SELECT note_text FROM productnotes WHERE note_text LIKE '%rabbit%'; 
```

- 但是却与全文本搜索，各有优劣


1. 
2.  在使用全文本搜索时就会对此结果排序，但是like却不会。

# 全文本布尔操作符

+ +包含，词必须存在
- -排除，词必须不出现
- 大于号 包含，而且增加等级值
- <包含，且减少等级值
- () 把词组成子表达式(允许这些子表达式作为一个组被包含，排除，排列等）
- ~取消一个词的排序值
* *词尾的通配符
* “” 定义一个短语

## 布尔文本搜索

布尔方式搜索，添加布尔操作符

IN BOOLEAN MODE

* 举几个例子：

* ```c
  1 SELECT note_text FROM productnotes WHERE Match(note_text) Against('+rabbit +bait' IN BOOLEAN MODE);
  /*这个搜索匹配包含词rabbit和bait的行 */
  2 SELECT note_text FROM productnotes WHERE Match(note_text) Against('rabbit bait' IN BOOLEAN MODE);
  /*没有指定操作符，这个搜索匹配包含rabbit 和bait中的至少一个词的行。*/
  3 SELECT note_text FROM productnotes WHERE Match(note_text) Against('"rabbit bait"' IN BOOLEAN MODE);
  4 SELECT note_text FROM productnotes WHERE Match(note_text) Against ('>rabbit <carrot' IN BOOLEAN MODE);
  ```

  

