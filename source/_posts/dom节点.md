---
title: dom节点
date: 2020-06-18 09:01:06
tags: html
categories: html
---

## 概述

> 本章介绍

<!--more-->

## 正文

1 

![](https://photos.alitaalice.cn/image/20200618090133.png)

2 ![](https://photos.alitaalice.cn/image/20200618090722.png)

3 article 和 aside 是 html5 的新标签。前段时间我刚学 html5 ，也是看的视频，刚开始不太明白，后来也想通了。html5 是什么呢？是 html 的升级版，在标签和功能上增强了，说到底还是 html 。html 又是什么呢？html 只是标签，a 就是锚点，p 就是段落，img 就是图片，我们按照这些规定来组织页面，他们本身只是标签，除此之外，没有任何意义，标签的背景颜色是什么，那是 css 的事，标签点击后出现什么效果，那时 js 的事。html 标签有几种分类，其中有一种就是网页布局性质的标签，如最常用的 div。抛开以前的传统网页布局（table布局）不谈，就说现在的网页布局——div+css。你比如说，你要做一个最简单的一行两列的网页，外层是一个 div 容器，里面两个 div，左边是导航菜单，右边是内容，为了实现网页布局，你肯定得用 css 定位，为了方便定位，你肯定得为 div 设置 id 或者 class，我们暂且用 id。外层容器 div ：id="wrap"，内层左边 div：id="aside"，内层右边 div：id="article"。为什么左边导航 id 要给它设置为 aside（旁边），而不用 div1、div2 呢？因为 aside 赋予了 div 意义，给当前开发者和后期维护者带来方便，一看到 <div id="aside"> 我就知道它的作用，看到 <div id="div1"> 谁知道这是什么东西，就像 div 标签本身一样，毫无意义。而 article 和 aside 就像 div 一样，只是布局标签，除了标签名字不一样，其他功能意义基本是一样的，article、aside 里面的字体、背景、边框等没有任何特殊的样式，也不是鼠标点击了 aside 标签之后会出现什么特殊的效果，因为它们只是简简单单的标签。既然功能和 div 一模一样，html5 为何多此一举，又生产出几个多余的 “div” 出来呢？有句话叫做：存在的就是合理的。因为很多网站布局是重复的，全世界网站有很多都是左边是导航，右边是正文内容，然后给div设置id来用css布局，因为有这个需求，html5 就人性化的添加了几个标签，从而简化了开发人员的开发，毕竟，<aside> 与 <div id="aside">，那个更好？html 角度：前者比后者少写几行代码，一定程度简化了网页文件大小。css 角度：前者直接使用 aside 就能获取到标签，后者需要通过 id 。js 角度：同上。之前也听说过这么一个消息，说一些移动设备（如 ipad），在解析 html5 标签时，遇到 aside 标签可能会有个性化的展示，可能效果更美观。总结：<article> 你就看做是 <div id="article">，<aside> 你就看做是 <div id="aside">，仅仅是人为的给div 换了一个说话，换汤不换药，还是 div 。

4 ul  无序列表

<a> 标签中的target=_blank

_self相同框架
_top整页
_blank新建一个窗口
_parent父窗口
其它的就是自定义了，可以指向已有的窗口名称

![](https://photos.alitaalice.cn/image/20200619085109.png)