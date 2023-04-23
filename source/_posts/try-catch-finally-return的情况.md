---
title: try_catch_finally_return的情况
date: 2020-05-28 22:55:58
tags: JAVASE
categories: JAVASE
---

## 概述

> 本章介绍try_catch_finally_return的情况

<!--more-->

## 正文

## try-catch

```java
try
{
  code
}
catch(ExceptionType e)
{
handler for this type
}
```

如果try 语句块中的任何代码抛出了catch 子句中指定的一个异常类

那么

1程序将跳过try  语句块

2程序将执行catch语句块



```java
public void read(String filename) throws IOException
{
 code
}
```

方法的首部添加一个throws说明符，提醒调用者这个方法可能会抛出异常

## finally

代码抛出一个异常时，就会停止处理这个方法中的剩余代码，并且退出这个方法，如果这个方法已经获得了只有它自己知道的一些本地资源，而且这些资源必须清理，finally子句可以解决这个问题。

```java
try
{
code
}
catch(IOException e)
{
show error message
}
finally
{
in.close();
}
```

## try-with-resource

```java
try
{
work with the resource
}
finally
{
close the resource
}
/*可以用try-with-resource代替 */
try(Resource res=...)
{
    work with res
}
try块退出时，会自动调用res.close()
```

