---
title: tcp三次握手
date: 2020-09-09 20:47:15
tags:
categories:
---

## 概述

> 本章介绍

<!--more-->

## 正文

SYN表示建立连接，

FIN表示关闭连接，

ACK表示响应

第一次握手：主机A发送位码为syn＝1，随机回产生seq number=1234567的数据包到服务答器，主机B由SYN=1知道，A要求建立联机；

第二次握手：主机B收到请求后要确认联机信息，向A发送ack number=(主机A的seq+1)，syn=1，ack=1，随机产生seq=7654321的包；
第三次握手：主机A收到后检查ack number是否正确，即第一次发送的seq number+1，以及位码ack是否为1，若正确，主机A会再发送ack number=(主机B的seq+1)，ack=1，主机B收到后确认seq值与ack=1则连接建立成功。 完成三次握手，主机A与主机B开始传送数据。