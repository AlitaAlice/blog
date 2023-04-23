---
title: JAVA注解
date: 2020-05-11 14:49:56
tags: JAVASE
categories: 面试
---

## 概述

> 本章介绍 JAVA注解

<!--more-->

## 正文

## 1.注解的概述

注解的语法： @注解名称

注解的作用:  替代xml配置文件

我们以前总是要写一些配置文件，如web.xml 里面要写<servlet> 和<sevlet-mapping>

tomcat用来读取配置文件

而在servlet3.0中可以使用注解来代替配置文件，@WebServlet 用来代替该配置文件

##  2. JAVA中的注解

- @Override
- @Deprecated: 作用在方法上，标记该方法为作废方法 （已经过时的方法）
- @SuppressWarning :作用在方法上，压制警告@SuppressWarnings("all")压制所有警告

## 3. 注解的使用

- 定义注解类：框架的工作
- 使用注解类：我们的工作
- 读取注解（反射）：框架的工作

## 4.自定义注解类

**@interface**

eg:

```java
public @interface MyAnn{}
```

## 5.使用注解的目标

注解可以使用在类（接口或者枚举），属性，方法，构造器，包，参数，局部变量

eg:

```java
@MyAnn
public class MyClass
{
@MyAnn
private int a;
@MyAnn
public MyClass()
{}
@MyAnn
public void fun1()
{}
@MyAnn
public void fun2(@MyAnn String s)
{
    @MyAnn
    int n=10;
}
}
```

## 6.注解的属性

定义注解时，也可以给出属性

```java
public @interface MyAnn
{
String value();  default "hello world"
int value1();
}
```

其中value就是属性，你可能会说value是一个方法，没错，它是一个方法，但是我们非要称之为属性，是因为把它当作属性更好理解:

eg:

```java
@MyAnn(value1=100,value="hello")
public class MyClass
{}
```

- 注解的属性后面要有一对圆括号，而且圆括号内不能给出东西。就像是无参的方法一样；
  注解的属性类型只能是：基本类型、String、Enum、Class、注解类型、以上类型的一维数组类型；
  注解的属性可以有默认值，例如：int a() default 100;
  数组的属性默认值：int[] arr() default {1,2,3}，这里不能使用new int[]{1,2,3}
  使用注解时，在给数组属性赋值时的格式：@MyAnn(arr={1,2,3})；

## 7.元注解

**元注解：用于描述注解的注解**

@Target ：描述注解作用的位置

- ElementType取值：
- TYPE：作用在类上
- METHOD ：作用在方法上
- FIELD ：作用在成员变量上

eg：

Target 注解的源码：

```java
public @interface Target {  
    ElementType[] value();  
}  
public enum ElementType {  
  TYPE,FIELD,METHOD,PARAMETED,CONSTRUCTOR,LOCAL_VARIABLE,ANNOCATION_TYPE,PACKAGE  
}  
```

在定义注解时，可以使用@Target 注解来限制注解的作用目标

```java
@Target({ElementType.TYPE,ElementType.METHOD})
public @interface MyAnn
{}  /* 该注解定义在类和方法上 */
@MyAnn()  
public class MyClass {  
    @MyAnn()  //报错  
    private int a;  
      
    @MyAnn()  
    public void fun() {}  
} 
```

## 8.注解的保留策略

- 注解的保留策略是指

  - 注解保留在源代码（SOURCE)上
  - 注解保留在class文件上（CLASS）
  - 注解保留在类运行时（RUNTIME），可以被类加载器加载到内存中

- 如果希望注解被反射，那么注解就是保留到运行时，而不是源代码或者类文件上

- 指定注解的保留策略需要使用元注解@Retention ，它有一个value属性，类型为RetentionPolicy

  RetentionPolicy是枚举类型

  ```java
  public @interface Retention {  
      RetentionPolicy value();  
  }  
  public enum RetentionPolicy {  
      SOURCE, CLASS, RUNTIME  
  } 
  ```

  eg：指定注解保留到运行时

  ```java
  @Retention(RetionOPlicy.RUNTIME)
  @Target({ElementType.TYPE,ElementType.METHOD})
  public @interface MyAnn
  {
  String value() default "hello";
  int value1() default 100;
  }
  ```

## 9.注解处理器

