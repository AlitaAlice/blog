---
title: XPath的使用
date: 2020-06-21 22:52:50
tags: 爬虫
categories: 爬虫
---

## 概述

> 本章介绍XPath

<!--more-->

## 正文

## XPath的使用

XPath，全称 XML Path Language，即 XML 路径语言，它是一门在XML文档中查找信息的语言。XPath 最初设计是用来搜寻XML文档的，但是它同样适用于 HTML 文档的搜索。

所以在做爬虫时，我们完全可以使用 XPath 来做相应的信息抽取，本节我们来介绍一下 XPath 的基本用法。

## 1. XPath概览

XPath 的选择功能十分强大，它提供了非常简洁明了的路径选择表达式，另外它还提供了超过 100 个内建函数用于字符串、数值、时间的匹配以及节点、序列的处理等等，几乎所有我们想要定位的节点都可以用XPath来选择。

XPath 于 1999 年 11 月 16 日 成为 W3C 标准，它被设计为供 XSLT、XPointer 以及其他 XML 解析软件使用，更多的文档可以访问其官方网站：[https://www.w3.org/TR/xpath/](https://link.zhihu.com/?target=https%3A//www.w3.org/TR/xpath/)。

## 2. XPath常用规则

我们现用表格列举一下几个常用规则：

表达式描述
nodename选取此节点的所有子节点
/从当前节点选取直接子节点
//从当前节点选取子孙节点
.选取当前节点
..选取当前节点的父节点
@选取属性

在这里列出了XPath的常用匹配规则，例如 / 代表选取直接子节点，// 代表选择所有子孙节点，. 代表选取当前节点，.. 代表选取当前节点的父节点，@ 则是加了属性的限定，选取匹配属性的特定节点。

例如：

```text
//title[@lang=’eng’]
```

这就是一个 XPath 规则，它就代表选择所有名称为 title，同时属性 lang 的值为 eng 的节点。

在后文我们会介绍 XPath 的详细用法，通过 Python 的 LXML 库利用 XPath 进行 HTML 的解