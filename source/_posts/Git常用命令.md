---
title: Git常用命令
date: 2020-06-03 21:49:05
tags: Git
categories: Git
---

## 概述

> 本章介绍

<!--more-->

## 正文

初始化仓库

```java
git init 
```

查看仓库的状态

```
git status
```

向暂存区添加文件

```
git add
```

保存仓库的历史记录

```java
git commit -m "first commit"
```

查看提交日志

```java
git log
```

查看更改前后的差别

```
git diff
```

显示分支一览表

```java
git branch
```

创建、切换分支

```
git checkout -b alita
/* 创建名为alita的分支 */ 
```

合并分支

```
git checkout master
/* 为了在历史记录中明确记录下本次分支合并。我们需要创建合并并提交 */
git merge --no-ff alita
```

以图表形式查看分支

```
git log --graph
```

添加远程仓库

```
git remote add origin git@github.com:xxx
```

推送至远程仓库

```java
git push -u origin master
```

从远程仓库获取

```
git clone git@xxx
```

获取最新的远程仓库分支

```java
git pull origin alita
```

