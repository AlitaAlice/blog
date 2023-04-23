---
title: jQuery入门
date: 2020-06-13 11:01:39
tags: jQuery
categories: jQuery
---

## 概述

> 本章介绍jQuery入门

<!--more-->

## 正文

### 1 什么是 jQuery ？

jQuery是一个JavaScript函数库。

jQuery是一个轻量级的"写的少，做的多"的JavaScript库。

jQuery库包含以下功能：

- HTML 元素选取
- HTML 元素操作
- CSS 操作
- HTML 事件函数
- JavaScript 特效和动画
- HTML DOM 遍历和修改
- AJAX
- Utilities

**提示：** 除此之外，Jquery还提供了大量的插件。

2 jQuery语法

基础语法：$(selector)查询和查找HTML元素

jQuery的action()执行对元素的操作

实例：

```
$(this).hide() //隐藏当前元素
$("p").hide() //隐藏所有<p>元素
$("p.test").hide()  //隐藏所有class="test"的p元素
$("#test").hide() //隐藏id="test"的元素
```

### 2文档就绪事件

这是为了防止文档在完全加载（就绪）之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作。

如果在文档没有完全加载之前就运行函数，操作可能失败。下面是两个具体的例子：

- 试图隐藏一个不存在的元素
- 获得未完全加载的图像的大小

jQuery函数位于一个document ready函数中

```javascript
$(document).ready(function()
{
//开始写jQuery代码
});
```

简洁写法

```javascript
$(function())
{
//开始写jQuery代码...
});
```

### 3 元素选择器

 jQuery元素选择器基于元素名选取元素

在页面中选取所有的<p>元素

$("p")

```
$(document).ready(function()
{
$("button").click(function())
{
$("p").hide();
})
}
```

### 4 id 选择器

选择器通过HTML元素的id属性选取指定的元素

语法为

```javascript
$("#test")
```

实例

```javascript
$(document).ready(function()
{
$("button").click(function(){
$("#test").hide();
});
});
<body>
<h2>这是一个标题</h2>
<p>这是一个段落</p>
<p id="test">这是另外一个段落</p>
<button>点我</button>
</body>
```

### 5 .class选择器

语法为

$(".test")

实例 用户点击按钮后所有带有class=“test”属性元素都隐藏：

```javascript
$(document).ready(function()
{
$("button").click(function()
{
$(".test").hide();
});
});
<h2 class="test">这是一个标题</h2>
<p class="test">这是一个段落。</p>
```

![](https://photos.alitaalice.cn/image/20200613124742.png)

click()方法是当按钮点击事件被触发时调用的一个函数

```javascript
$("p").click(function()
{
$(this).hide();
});
```

focus()

当元素获得焦点时，发生 focus 事件。

当通过鼠标点击选中元素或通过 tab 键定位到元素时，该元素就会获得焦点。

focus() 方法触发 focus 事件，或规定当发生 focus 事件时运行的函数：

```javascript
$("input").focus(function()
{
$(this).css("background-color","#ccccc");
});
```

blur()

```javascript
$("input").blur(function()
{
$(this).css("background-color","#ffffff");
});
```

```javascript
<script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js">
</script>
<script>
$(document).ready(function(){
  $("input").focus(function(){
    $(this).css("background-color","#cccccc");
  });
  $("input").blur(function(){
    $(this).css("background-color","#ffffff");
  });
});
</script>
</head>
<body>

Name: <input type="text" name="fullname"><br>
Email: <input type="text" name="email">

</body>
```

p

![](https://photos.alitaalice.cn/image/20200709093404.png)



















67.