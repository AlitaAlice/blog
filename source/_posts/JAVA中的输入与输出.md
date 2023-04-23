---
title: JAVA中的输入与输出
date: 2020-05-06 13:12:52
tags: JAVASE
categories: JAVASE
---

#  JAVA中的输入

## 读取输入  

  要想通过输入台进行输入，首先需要构造一个与“标准输入流”System.in关联的Scanner对象。
  <!--more-->

```java
Scanner scanner=new Scanner(System.in);
```

Scanner类中的方法：

API  JAVA.util.Scanner

| String nextLine()       | 读取输入的下一行内容  以enter作为结束符  能得到带空格的字符串 |
| ----------------------- | ------------------------------------------------------------ |
| String next()           | 读取输入的下一个单词（以空格作为分隔符）空格视而不见         |
| int nextInt()           | 只读取int值                                                  |
| double nextDouble()     | 只读取double值                                               |
| boolean hasNext()       | 检测输入中是否还有其他的单词                                 |
| boolean hasNextInt()    | 检测输入中是否还有表示整数                                   |
| boolean hasNextDouble() | 检测输入中是否还有表示浮点数                                 |

