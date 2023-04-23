---
title: Spring起步
date: 2020-05-10 11:58:43
tags: Spring
categories: 框架
---

## 概述

> 本章介绍什么是Spring

<!--more-->

## 正文

## 什么是Spring

- Spring 的核心是提供一个容器(container) 

  通常称为Spring 应用上下文（Spring application context) 应用前后关系，它们会创建和管理应用组件。

  这些组件也被称为是bean ，会在Spring应用上下文中装配在一起，从而形成一个完整的应用程序。

  这就像砖块，砂浆，木材 ，管道等组合在一起



- 将bean装配在一起是通过一种基于依赖注入（dependency injection DI)

  举例来说：假设在众多的组件中，有俩个是我们需要处理的：库存服务，和商品服务。

  商品服务需要依赖于库存服务。

  如图所示阐述了bean和Spring 应用上下文之间的关系。

  ![](TIM图片20200510124205.png)
  
  依赖注入到需要它们的bean中，另外使用依赖注入的应用依赖于单独的实体（容器）来创建和维护所有的组件。
  
   Spring Initializr 是一个基于浏览器的web应用，能够生成Spring 项目结构的骨架。

### pom文件

## Springboot的引导类

@SpringBootApplication  ：是一个组合注解，包括：

- @SpringBootConfiguration

将该类声明为配置类

- @EnableAutoConfiguration

启动Spring BOOT 的自动配置 

- @ComponentScan 

启动组件扫描

@Component @Controller @Service 注解声明其他类，Spring会自动发现它们并将它们注册为Spring应用上下文的组件。