---
title: Collection
date: 2020-05-06 10:30:29
tags: JAVA集合
categories: JAVA集合
---

## Java容器可分为两大类：

- Collection接口 继承JAVA.lang.Object

  - List接口
    - **ArrayList**
    - LinkedList
	<!--more-->
    - Vector(了解，已过时)
  - Set接口
    - HashSet
      - LinkedHashSet
    - TreeSet

- Map接口  继承JAVA.lang.Object

  - **HashMap**

    - LinkedHashMap

  - TreeMap

  - ConcurrentHashMap

  - Hashtable(了解，，已过时)

## Collection接口：

- Collection接口的常用方法

- 添加功能

  - | boolean add(Object obj)       | 添加一个元素       |
    | ----------------------------- | ------------------ |
    | boolean  addAll(Collection c) | 添加一个集合的元素 |

    示例：

    ```java
       static Collection c = new ArrayList();
    
        public static void main(String[] args) {
            System.out.println("add:"+c.add("hello"));
        }
    /* 输出为 add:true */
    ```

​             

```java
static Collection c1 = new ArrayList();
    static Collection c2 = new ArrayList();

    public static void main(String[] args) {
        c1.add("xxxx");
        System.out.println("add:" + c1.add("hello"));
        System.out.println("addAll:" + c2.addAll(c1));
    }
/* 输出add:true
addAll:true */ 
```

- 删除功能

  - | void clear()                | 移除所有元素           |
    | --------------------------- | ---------------------- |
    | boolean remove(Object o)    | 移除一个元素           |
    | boolean removeAll(Object o) | 移除一个集合的所有元素 |

    

- 判断功能

  - | boolean contains(Object o)    | 判断集合中是否包含指定的元素                           |
    | ----------------------------- | ------------------------------------------------------ |
    | boolean containsAll(Object o) | 判断集合中是否包含指定的集合元素（一个集合中的所有元素 |
    | boolean isEmpty()             | 判断集合是否为空                                       |

- **获取功能**

  重点：迭代器（Iterator） 下一篇中我们详细解释。

  itetator()   返回在此 Collection 的元素上进行迭代的迭代器。用于遍历集合中的对象
  
  ```java
  import java.util.ArrayList;
  import java.util.Collection;
  import java.util.Iterator;
  
  
  public class Muster {
      public static void main(String[] args) {
          Collection<String> list=new ArrayList<>();
          list.add("a");
          list.add("b");
          list.add("c");
          Iterator<String> it=list.iterator();
          while(it.hasNext())
          {
              String str=(String) it.next();
              System.out.println(str);
          }
      }
  }
  ```
  
  