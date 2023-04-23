---
title: '@RequestBody的用法'
date: 2020-06-15 22:55:26
tags: springmvc
categories: springmvc
---

## 概述

> 本章介绍@RequestBody的用法

<!--more-->

## 正文

https://jingyan.baidu.com/article/624e7459069f4034e8ba5a87.html

```java
<script>
jsonData();
function jsonData()
{
    $.ajax({
        url:"<%=path%>/user/jsonTest.do"
        contentType:'application/json;charset=utf8',
        data:'{"username":"张三","address":"福州"}，
        type:'post',
        success:function(data)
        {
            alert(data);
        },error:function(error)
        {
           alert(error);}
    })
}
```

```java
后台接收如下：
@RequestMapping("/jsonTest.do")
public void jsonTest(@RequstBody User user) throws Exception
{
sout(user.toString());
}
```

```
那么输出的user就为 User[id=0,username=张三,sex= ,birthday=null,address=福州]
```

可以看到User这个对象中的username和address都已经自动赋值好了，这个就是json格式的数据转java对象了，是不是很方便呢，可以省去我们在后台将json转成java对象。不过在使用的时候，我们要注意两边的名称要相同，前台的username要对应java对象中的username这样才能成功。否则得到如下：

![](https://photos.alitaalice.cn/image/20200616100452.png)