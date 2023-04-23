---
title: I/O
date: 2020-07-09 21:10:17
tags: JAVASE
categories: JAVASE
---

## 概述

> 本章介绍I/O

<!--more-->

## 正文

# 字符流和字节流

- 字节流：一次读入或读出是8位二进制。
- 字符流：一次读入或读出是16位二进制。

**设备上的数据无论是图片或者视频，文字，它们都以二进制存储的。二进制的最终都是以一个8位为数据单元进行体现，所以计算机中的最小数据单元就是字节。意味着，字节流可以处理设备上的所有数据，所以字节流一样可以处理字符数据。**

#### **结论：只要是处理纯文本数据，就优先考虑使用字符流。 除此之外都使用字节流。**

# 输入流和输出流

## 输入字节流 InputStream

- `InputStream` 是所有的输入字节流的父类，它是一个抽象类。
- `ByteArrayInputStream`、`StringBufferInputStream`、`FileInputStream` 是三种基本的介质流，它们分别从`Byte 数组`、`StringBuffer`、和`本地文件`中读取数据。
- `PipedInputStream` 是从与其它线程共用的管道中读取数据，与Piped 相关的知识后续单独介绍。
- `ObjectInputStream` 和所有`FilterInputStream` 的子类都是装饰流（装饰器模式的主角）。

## 输出字节流 OutputStream

- `OutputStream` 是所有的输出字节流的父类，它是一个抽象类。
- `ByteArrayOutputStream`、`FileOutputStream` 是两种基本的介质流，它们分别向`Byte 数组`、和`本地文件`中写入数据。
- `PipedOutputStream` 是向与其它线程共用的管道中写入数据。
- `ObjectOutputStream` 和所有`FilterOutputStream` 的子类都是装饰流。

**总结：**

- 输入流：InputStream或者Reader：从文件中读到程序中；

- 输出流：OutputStream或者Writer：从程序中输出到文件中；

- # 装饰流使用

  ​     除了按照流的方向可以把流划分为输入流和输出流两类，按照流读写数据的基本单位把流划分为字节流和字符流两类以外，还可以按照流是否直接连接实际数据源，例如文件、网络、字节数组等，将流又可以划分为实体流和装饰流两大类。

  ​     其中实体流指直接连接数据源的流类，如前面介绍的**FileInputStream/FileOutputStream**和**FileReader和FileWriter**，该类流直接实现将数据源转换为流对象，在实体流类中实现了流和数据源之间的转换，实体流类均可单独进行使用。

  ​     而装饰流指不直接连接数据源，而是以其它流对象(实体流对象或装饰流对象)为基础建立的流类，该类流实现了将实体流中的数据进行转换，增强流对象的读写能力，比较常用的有DataInputStream/DataOutputStream和BufferedReader/BufferedWriter等，装饰流类不可以单独使用，必须配合实体流或装饰流进行使用。

  ​     

# 流必须要关闭的原因

java相对C,C++来说不需要手动释放内存,在对象引用被消除之后,正常情况下内存资源是会被垃圾回收,那么在使用完IO流之后为什么需要手动关闭.
这是**为了回收系统资源**,比如**释放占用的端口,文件句柄,网络操作数据库应用**等.对Unix系统来说,所有的资源都可以抽象成文件,所以可以通过lsof来观察。

看下面这个例子,我们创建许多的IO流，但是不关闭

```java
public class Hello {
    public static void main(String[] args) throws Exception {
        for (int i = 0; i < 100; i++) {
            FileInputStream is = new FileInputStream("/tmp/data/data"+i);
            byte[] bs = new byte[512];
            int len;
            while ((len = is.read(bs)) != -1) ;
            Thread.sleep(1000L);
        }
        Thread.sleep(10000L);
    }
}
```

运行这个程序之后,使用losf命令查看相关的文件句柄,会发现文件句柄始终在增长,当积累到一定时间之后会出现too many open files错误

# 举例

```java
package com.alita.demo.controller;

import java.io.FileInputStream;

/**
 * Title:
 * Description:
 * Company:
 *
 * @author im.alitaalice@gmail.com
 * @date Created in 20:08 2020/8/19
 */
public class FileInputStreamController {

    public static void main(String[] args) {
        FileInputStreamController fileInputStreamController = new FileInputStreamController();
        String filePath = "E:/Demo/abc.txt";
        String result = fileInputStreamController.readFile(filePath);
        System.out.println(result);

    }

    public String readFile(String filePath) {

        FileInputStream fileInputStream = null;
        String result = "";

        try {
            fileInputStream = new FileInputStream(filePath);
            /**
             * available():返回与之关联的文件的字节数
             */
            int lenth = fileInputStream.available();
            byte[] array = new byte[lenth];
            /**
             * 把数据读到数组中去
             */
            fileInputStream.read(array);


            /**
             * 根据获取到的Byte数组新建一个字符串，然后输出
             */
            result = new String(array);

        } catch (Exception e) {
            e.printStackTrace();
        }
        finally {
            try
            {
                fileInputStream.close();
            }
            catch (Exception e)
            {
                e.printStackTrace();
            }
        }
        return result;
    }
}
############################
    abcsdadasd

Process finished with exit code 0
```

```java
package com.alita.demo.controller;

import java.io.FileOutputStream;

/**
 * Title:
 * Description:
 * Company:
 *
 * @author im.alitaalice@gmail.com
 * @date Created in 20:33 2020/8/19
 */
public class FileOutputSteamController {
    public static void main(String[] args) {
        FileOutputSteamController fileOutputSteamController = new FileOutputSteamController();
        String filePath = "E:/Demo/abc.txt";
        String content = "今天天气很好，hello world";
        /**
         * it will replace
         */
        fileOutputSteamController.writeFile(filePath, content);
    }



    public void writeFile(String filePath, String content) {
        FileOutputStream fileOutputStream = null;
        try{
            fileOutputStream = new FileOutputStream(filePath);

            byte[] array = content.getBytes();

            /**
             * array写入到filePath
             */
            fileOutputStream.write(array);
        }
        catch (Exception e)
        {
            e.printStackTrace();
        }
        finally {
            try
            {
                fileOutputStream.close();
            }
            catch (Exception e)
            {
                e.printStackTrace();
            }
        }
    }
}
#############################
    今天天气很好，hello world
```

