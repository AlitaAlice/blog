---
title: java中的引用
date: 2020-08-31 16:19:00
tags: javase
categories: javase
---

## 概述

> 本章介绍java中的引用

<!--more-->

## 正文

1前言：先理解变量

在我们弄清楚引用之前，我们还得从变量讲起：

### 变量有两类关键

（1）变量类型

- 基本类型
- 引用类型

（2）变量形态

- 局部变量
- 形参
- 属性
- 静态变量

一个变量是由它的类型和形态决定的，也就是上边两类的笛卡尔积。

### 变量的存储位置

**变量在内存中的哪个区域存储，是由它的形态决定的，不是类型决定的！！！**
在我们判断一个变量在那里存储时，先看它属于什么（属于对象，属于类等等）然后再判断它应该在什么位置上放着（属于对象就在堆上，属于类就在方法区等等）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421165622947.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0ODQwMTQ4,size_16,color_FFFFFF,t_70)

## 再谈引用

### 基本数据类型与引用类型的区别

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421170403278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0ODQwMTQ4,size_16,color_FFFFFF,t_70)

### 对引用的比喻

基本数据类型说是一个文件的话.，引用数据类型就是那个文件的快捷方式，通过引用我们就可以找到那个对象。

# == 和 equals 的区别

## 1、== 解读

对于基本类型和引用类型 == 的作用效果是不同的，如下所示：

- 基本类型：比较的是值是否相同；
- 引用类型：比较的是引用是否相同；

代码示例：

```
String x = "string";
String y = "string";
String z = new String("string");
System.out.println(x==y); // true
System.out.println(x==z); // false
System.out.println(x.equals(y)); // true
System.out.println(x.equals(z)); // true
复制代码
```

代码解读：因为 x 和 y 指向的是同一个引用，所以 == 也是 true，而 new String()方法则重写开辟了内存空间，所以 == 结果为 false，而 equals 比较的一直是值，所以结果都为 true。

## 2、equals 解读

equals 本质上就是 ==，只不过 String 和 Integer 等重写了 equals 方法，把它变成了值比较。看下面的代码就明白了。

首先来看默认情况下 equals 比较一个有相同值的对象，代码如下：

```
class Cat {
    public Cat(String name) {
        this.name = name;
    }

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

Cat c1 = new Cat("王磊");
Cat c2 = new Cat("王磊");
System.out.println(c1.equals(c2)); // false
复制代码
```

输出结果出乎我们的意料，竟然是 false？这是怎么回事，看了 equals 源码就知道了，源码如下：

```
public boolean equals(Object obj) {
		return (this == obj);
}
复制代码
```

原来 equals 本质上就是 ==。

那问题来了，两个相同值的 String 对象，为什么返回的是 true？代码如下：

```
String s1 = new String("老王");
String s2 = new String("老王");
System.out.println(s1.equals(s2)); // true
复制代码
```

同样的，当我们进入 String 的 equals 方法，找到了答案，代码如下：

```
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
复制代码
```

原来是 String 重写了 Object 的 equals 方法，把引用比较改成了值比较。

## 3、总结

**总体来说，== 对于基本类型来说是值比较，对于引用类型来说是比较的是引用；而 equals 默认情况下是引用比较，只是很多类重写了 equals 方法，比如 String、Integer 等把它变成了值比较，所以一般情况下 equals 比较的是值是否相等。**

