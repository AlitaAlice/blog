---
title: ACID
date: 2020-09-09 17:07:52
tags: mysql
categories: mysql
---

## 概述

> 本章介绍mysql事务acid

<!--more-->

## 正文

# ACID

事务具有4个特征，分别是原子性、一致性、隔离性和持久性，简称事务的ACID特性；

# 一、原子性（atomicity)

一个事务要么全部提交成功，要么全部失败回滚，不能只执行其中的一部分操作，这就是事务的原子性

# 二、一致性（consistency)

事务的执行不能破坏数据库数据的完整性和一致性，一个事务在执行之前和执行之后，数据库都必须处于一致性状态。

如果数据库系统在运行过程中发生故障，有些事务尚未完成就被迫中断，这些未完成的事务对数据库所作的修改有一部分已写入物理数据库，这是数据库就处于一种不正确的状态，也就是不一致的状态

# 三、隔离性（isolation）

**事务的隔离性是指在并发环境中，并发的事务时相互隔离的，一个事务的执行不能不被其他事务干扰。**不同的事务并发操作相同的数据时，每个事务都有各自完成的数据空间，即一个事务内部的操作及使用的数据对其他并发事务时隔离的，并发执行的各个事务之间不能相互干扰。

在标准SQL规范中，定义了4个事务隔离级别，不同的隔离级别对事务的处理不同，分别是：未授权读取，授权读取，可重复读取和串行化

1、读未提交（Read Uncommited），该隔离级别允许脏读取，其隔离级别最低；比如事务A和事务B同时进行，事务A在整个执行阶段，会将某数据的值从1开始一直加到10，然后进行事务提交，此时，**事务B能够看到这个数据项在事务A操作过程中的所有中间值**（如1变成2，2变成3等），而对这一系列的中间值的读取就是未授权读取

2、授权读取也称为已提交读（Read Commited），**授权读取只允许获取已经提交的数据**。比如事务A和事务B同时进行，事务A进行+1操作，此时，事务B无法看到这个数据项在事务A操作过程中的所有中间值，只能看到最终的10。另外，如果说有一个事务C，和事务A进行非常类似的操作，只是事务C是将数据项从10加到20，此时事务B也同样可以读取到20，即授权读取允许不可重复读取。

3、可重复读（Repeatable Read)

**就是保证在事务处理过程中，多次读取同一个数据时，其值都和事务开始时刻是一致的**，因此该事务级别禁止不可重复读取和脏读取，但是有可能出现幻影数据。所谓幻影数据，就是指同样的事务操作，在前后两个时间段内执行对同一个数据项的读取，可能出现不一致的结果。在上面的例子中，可重复读取隔离级别能够保证事务B在第一次事务操作过程中，始终对数据项读取到1，但是在下一次事务操作中，即使事务B（注意，事务名字虽然相同，但是指的是另一个事务操作）采用同样的查询方式，就可能读取到10或20；

4、串行化

是最严格的事务隔离级别，它要求所有事务被串行执行，即事务只能一个接一个的进行处理，不能并发执行。

# 四、持久性（durability）

事务一旦提交，其更改是永久性的，即使数据库系统崩溃也能恢复

保证持久性的策略就是**Write Ahead Logging**。在事务提交之前，备份一份事务的操作日志在磁盘上，备份成功再允许事务成功提交。



### 2.1 事务的隔离级别分为：

- Read uncommitted(读未提交)
- Read Committed(读已提交)
- Repeatable Reads(可重复读)
- Serializable(串行化)

#### Read uncommitted

`读未提交`：隔离级别最低的一种事务级别。在这种隔离级别下，会引发脏读、不可重复读和幻读。

#### Read Committed

`读已提交`读到的都是别人提交后的值。这种隔离级别下，会引发不可重复读和幻读，但避免了脏读。

#### Repeatable Reads

`可重复读`这种隔离级别下，会引发幻读，但避免了脏读、不可重复读。

#### Serializable

`串行化`是最严格的隔离级别。在Serializable隔离级别下，所有事务按照次序依次执行。脏读、不可重复读、幻读都不会出现。

![隔离级别](https://img2018.cnblogs.com/blog/1629488/201906/1629488-20190622123004301-566049444.png)

# 五、脏读，不可重复读，幻读

**1.** **脏读** ：脏读就是指当一个事务正在访问数据，并且对数据进行了修改，而这种修改还没有提交到数据库中，这时，另外一个事务也访问这个数据，然后使用了这个数据。

**2.** **不可重复读** ：是指在一个事务内，多次读同一数据。在这个事务还没有结束时，另外一个事务也访问该同一数据。那么，在第一个事务中的两 次读数据之间，由于第二个事务的修改，那么第一个事务两次读到的的数据可能是不一样的。这样就发生了在一个事务内两次读到的数据是不一样的，因此称为是不 可重复读。例如，一个编辑人员两次读取同一文档，但在两次读取之间，作者重写了该文档。当编辑人员第二次读取文档时，文档已更改。原始读取不可重复。如果 只有在作者全部完成编写后编辑人员才可以读取文档，则可以避免该问题。

**3.** **幻读** : 是指当事务不是独立执行时发生的一种现象，例如第一个事务对一个表中的数据进行了修改，这种修改涉及到表中的全部数据行。 同时，第二个事务也修改这个表中的数据，这种修改是向表中插入一行新数据。那么，以后就会发生操作第一个事务的用户发现表中还有没有修改的数据行，就好象 发生了幻觉一样。例如，一个编辑人员更改作者提交的文档，但当生产部门将其更改内容合并到该文档的主复本时，发现作者已将未编辑的新材料添加到该文档中。 如果在编辑人员和生产部门完成对原始文档的处理之前，任何人都不能将新材料添加到文档中，则可以避免该问题。