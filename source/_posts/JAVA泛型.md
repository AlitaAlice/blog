---
title: JAVA泛型
date: 2020-05-12 12:16:34
tags: JAVASE
categories: JAVASE
---

## 概述

> 本章介绍 [Java](http://lib.csdn.net/base/java)中的泛型

<!--more-->

## 正文

\1. [Java](http://lib.csdn.net/base/java)中的泛型是什么 ? 使用泛型的好处是什么?

这是在各种Java泛型[面试](http://yjbys.com/mianshi/)中，一开场你就会被问到的问题中的一个，主要集中在初级和中级面试中。那些拥有Java1.4或更早版本的开发背景的人 都知道，在集合中存储对象并在使用前进行类型转换是多么的不方便。泛型防止了那种情况的发生。它提供了编译期的类型安全，确保你只能把正确类型的对象放入 集合中，避免了在运行时出现ClassCastException。

\2. Java的泛型是如何工作的 ? 什么是类型擦除 ?

这是一道更好的泛型面试题。泛型是通过类型擦除来实现的，编译器在编译时擦除了所有类型相关的信息，所以在运行时不存在任何类型相关的信息。例如 List<String>在运行时仅用一个List来表示。这样做的目的，是确保能和[Java ](http://lib.csdn.net/base/java)5之前的版本开发二进制类库进行兼容。你无法在运行时访问到类型参数，因为编译器已经把泛型类型转换成了原始类型。根据你对这个泛型问题的回答情况，你会 得到一些后续提问，比如为什么泛型是由类型擦除来实现的或者给你展示一些会导致编译器出错的错误泛型代码。请阅读我的Java中泛型是如何工作的来了解更 多信息。

\3. 什么是泛型中的限定通配符和非限定通配符 ?

这是另一个非常流行的Java泛型面试题。限定通配符对类型进行了限制。有两种限定通配符，一种是<? extends T>它通过确保类型必须是T的子类来设定类型的上界，另一种是<? super T>它通过确保类型必须是T的父类来设定类型的下界。泛型类型必须用限定内的类型来进行初始化，否则会导致编译错误。另一方面<?>表 示了非限定通配符，因为<?>可以用任意类型来替代。更多信息请参阅我的文章泛型中限定通配符和非限定通配符之间的区别。

\4. List<? extends T>和List <? super T>之间有什么区别 ?

这和上一个面试题有联系，有时面试官会用这个问题来评估你对泛型的理解，而不是直接问你什么是限定通配符和非限定通配符。这两个List的声明都是 限定通配符的例子，List<? extends T>可以接受任何继承自T的类型的List，而List<? super T>可以接受任何T的父类构成的List。例如List<? extends Number>可以接受List<Integer>或List<Float>。在本段出现的连接中可以找到更多信息。

\5. 如何编写一个泛型方法，让它能接受泛型参数并返回泛型类型?

编写泛型方法并不困难，你需要用泛型类型来替代原始类型，比如使用T, E or K,V等被广泛认可的类型占位符。泛型方法的例子请参阅Java集合类框架。最简单的情况下，一个泛型方法可能会像这样:

public V put(K key, V value) {

return cache.put(key, value);

}

\6. Java中如何使用泛型编写带有参数的类?

这是上一道面试题的延伸。面试官可能会要求你用泛型编写一个类型安全的类，而不是编写一个泛型方法。关键仍然是使用泛型类型来代替原始类型，而且要使用JDK中采用的标准占位符。

\7. 编写一段泛型程序来实现LRU缓存?

对于喜欢Java编程的人来说这相当于是一次练习。给你个提示，LinkedHashMap可以用来实现固定大小的LRU缓存，当LRU缓存已经满 了的时候，它会把最老的键值对移出缓存。LinkedHashMap提供了一个称为removeEldestEntry()的方法，该方法会被put() 和putAll()调用来删除最老的键值对。当然，如果你已经编写了一个可运行的JUnit[测试](http://lib.csdn.net/base/softwaretest)，你也可以随意编写你自己的实现代码。

\8. 你可以把List<String>传递给一个接受List<Object>参数的方法吗？

对任何一个不太熟悉泛型的人来说，这个Java泛型题目看起来令人疑惑，因为乍看起来String是一种Object，所以 List<String>应当可以用在需要List<Object>的地方，但是事实并非如此。真这样做的话会导致编译错误。如 果你再深一步考虑，你会发现Java这样做是有意义的，因为List<Object>可以存储任何类型的对象包括String, Integer等等，而List<String>却只能用来存储Strings。

List<Object> objectList;

List<String> stringList;

objectList = stringList; //compilation error incompatible types

\9. Array中可以用泛型吗?

这可能是Java泛型面试题中最简单的一个了，当然前提是你要知道Array事实上并不支持泛型，这也是为什么Joshua Bloch在Effective Java一书中建议使用List来代替Array，因为List可以提供编译期的类型安全保证，而Array却不能。

\10. 如何阻止Java中的类型未检查的警告?

如果你把泛型和原始类型混合起来使用，例如下列代码，[java ](http://lib.csdn.net/base/java)5的javac编译器会产生类型未检查的警告，例如

List<String> rawList = new ArrayList()

注意: Hello.java使用了未检查或称为不安全的操作;

这种警告可以使用@SuppressWarnings(“unchecked”)注解来屏蔽。

Java泛型面试题补充更新:

我手头又拿到了几个Java泛型面试题跟大家分享下，这几道题集中在泛型类型和原始类型的区别上，以及我们是否可以用Object来代替限定通配符的使用等等：

Java中List<Object>和原始类型List之间的区别?

原始类型和带参数类型<Object>之间的主要区别是，在编译时编译器不会对原始类型进行类型安全检查，却会对带参数的类型进行检 查，通过使用Object作为类型，可以告知编译器该方法可以接受任何类型的对象，比如String或Integer。这道题的考察点在于对泛型中原始类 型的正确理解。它们之间的第二点区别是，你可以把任何带参数的类型传递给原始类型List，但却不能把List<String>传递给接受 List<Object>的方法，因为会产生编译错误。更多详细信息请参阅Java中的泛型是如何工作的。

Java中List<?>和List<Object>之间的区别是什么?

这道题跟上一道题看起来很像，实质上却完全不同。List<?> 是一个未知类型的List，而List<Object> 其实是任意类型的List。你可以把List<String>, List<Integer>赋值给List<?>，却不能把List<String>赋值给 List<Object>。   

List<?> listOfAnyType;

List<Object> listOfObject = new ArrayList<Object>();

List<String> listOfString = new ArrayList<String>();

List<Integer> listOfInteger = new ArrayList<Integer>();

listOfAnyType = listOfString; //legal

listOfAnyType = listOfInteger; //legal

listOfObjectType = (List<Object>) listOfString; //compiler error – in-convertible types

想了解更多关于通配符的信息请查看Java中的泛型通配符示例

List<String>和原始类型List之间的区别.

该题类似于“原始类型和带参数类型之间有什么区别”。带参数类型是类型安全的，而且其类型安全是由编译器保证的，但原始类型List却不是类型安全 的。你不能把String之外的任何其它类型的Object存入String类型的List中，而你可以把任何类型的对象存入原始List中。使用泛型的 带参数类型你不需要进行类型转换，但是对于原始类型，你则需要进行显式的类型转换。

List listOfRawTypes = new ArrayList();

listOfRawTypes.add(“abc”);

listOfRawTypes.add(123); //编译器允许这样 – 运行时却会出现异常

String item = (String) listOfRawTypes.get(0); //需要显式的类型转换

item = (String) listOfRawTypes.get(1); //抛ClassCastException，因为Integer不能被转换为String

List<String> listOfString = new ArrayList();

listOfString.add(“abcd”);

listOfString.add(1234); //编译错误，比在运行时抛异常要好

item = listOfString.get(0); //不需要显式的类型转换 – 编译器自动转换

这些都是Java泛型面试中 频繁出现的问题及其答案。所有这些面试题都不困难，其实它们都是基于泛型的基础知识。任何对泛型有不错了解的Java程序员都肯定熟知这些泛型题目。如果 你有任何好的面试题，不管是在什么面试中碰到的，或者如果你想知道任何Java泛型面试题的答案。