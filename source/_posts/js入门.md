---
title: js入门
date: 2020-06-13 07:13:23
tags: javascript
categories: javascript
---

## 概述

> 本章介绍javascript

<!--more-->

## 正文

### 1.为什么学习js

1. **HTML** 定义了网页的内容
2. **CSS** 描述了网页的布局
3. **JavaScript** 网页的行为

### 2.JavaScript：对事件的反应

<button type="button" onclick="alert('欢迎')"> 点我</button>

这是一个按钮，提醒按钮

### 3.JAVAScript：改变HTML内容

使用JAVAScript来处理HTML内容

```javascript
<body>
<h1>我的第一段JAVAScript</h1>
<p id="demo">
JAVAScript能改变HTML元素的内容
</p>
<script>
function myFunction()
{
x.document.getElementById("demo");//找到元素
x.innerHTML="hello javascript!";
}
</script>
<button type="button" onclick="myFunction()">点击这里</button>
</body>
```

### 3.验证输入

```javascript
<body>
<h1>我的第一段javaScrit</h1>
<p>请输入数字，如果不是数字那么，浏览器会弹出提示框</p>
<input id="demo" type="text">
<script>
function myFunction()
{
var x=document.getElementById("demo").value;
if(x==""||isNaN(x))
{
alert("不是数字");
}
}
</script>
<button type="button" onclick="myFunction()">点击这里</button>
</body>
</html>
```

### 4 在本例中，JavaScript 会在页面加载时向 HTML 的 <body> 写文本：![](https://photos.alitaalice.cn/image/20200613075951.png)

### 5<head> 中的 JavaScript 函数

```javascript
<!DOCTYPE html>
<html>
<head>
<script>
function myFunction()
{
    document.getElementById("demo").innerHTML="我的第一个 JavaScript 函数";
}
</script>
</head>
<body>
<h1>我的 Web 页面</h1>
<p id="demo">一个段落</p>
<button type="button" onclick="myFunction()">尝试一下</button>
</body>
</html>
```

6.<body> 中的 JavaScript 函数

```javascript
<!DOCTYPE html>
<html>
<body>
<h1>我的 Web 页面</h1>
<p id="demo">一个段落</p>
<button type="button" onclick="myFunction()">尝试一下</button>
<script>
function myFunction()
{
    document.getElementById("demo").innerHTML="我的第一个 JavaScript 函数";
}
</script>
</body>
</html>
```

7.外部的 JavaScript

```javascript
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
</body>
</html>
```

myScript.js 文件代码如下：

```javascript
function myFunction() {    document.getElementById("demo").innerHTML="我的第一个 JavaScript 函数"; }
```

```
JavaScript 显示数据
JavaScript 可以通过不同的方式来输出数据：

使用 window.alert() 弹出警告框。
使用 document.write() 方法将内容写到 HTML 文档中。
使用 innerHTML 写入到 HTML 元素。
使用 console.log() 写入到浏览器的控制台。
```

8.JavaScript 显示数据

```javascript
JavaScript 可以通过不同的方式来输出数据：

使用 window.alert() 弹出警告框。
使用 document.write() 方法将内容写到 HTML 文档中。
使用 innerHTML 写入到 HTML 元素。
使用 console.log() 写入到浏览器的控制台。
```

![](https://photos.alitaalice.cn/image/20200613082104.png)

