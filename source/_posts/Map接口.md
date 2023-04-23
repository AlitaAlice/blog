---
title: Map接口
date: 2020-05-08 19:57:52
tags: JAVA集合
categories: 后端
---

## 概述

> 本章介绍Map接口

<!--more-->

## 正文

## 一.Map的定义

Map是一种依照键（key）存储元素的容器，键（key）很像下标。在List里下标是整数，而在Map中键（key）可以是任意类型的对象。Map中不能有重复的键（key），每个键都有一个对应的值（value)

一个键（key）和它对应的值（value)构成Map集合中的一个元素。

Map中的元素是俩个对象，一个对象作为键，一个对象作为值，**键不可以重复，但是值可以重复。**

## 二.Map常用方法

- 添加

  | put(key,Value) | 调用put方法时，如果已经存在一个相同的key， 则返回的是前一个key对应的value，同时该key的新value覆盖旧value；如果是新的一个key，则返回的是null |
  | -------------- | ------------------------------------------------------------ |
  | putAll         | 从指定映射中将所有映射关系复制到此映射中去。                 |

- ![](https://photos.alitaalice.cn/image/20200530105616.png)

- 删除

  | remove(key)       | 删除指定key的键值对，返回被删除的key关联的value，不存在返回null |
  | ----------------- | ------------------------------------------------------------ |
  | remove(key,value) | 删除指定键值对，成功返回true                                 |
  | clear()           | 删除map中所有的键值对                                        |

- 获取

  | get(key)   | 返回指定key所对应的value，不存在则返回null |
  | ---------- | ------------------------------------------ |
  | Int size() | 获取长度                                   |

- 判断

  | boolean isEmpty()                   | 长度为0返回true，否则false    |
  | ----------------------------------- | ----------------------------- |
  | boolean containsKey(Object key)     | 判断集合中是否包含指定的key   |
  | boolean containsValue(Object value) | 判断集合中是否包含指定的value |

示例：

添加：

```java
package Set;

import java.util.HashMap;
import java.util.Map;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 13:48 2020/5/9
 */
public class Demo7 {
    public static void main(String[] args) {
        Map<String, Integer> map1 = new HashMap<>();
        map1.put("jack", 20);
        map1.put("rose", 18);
        map1.put("lucy", 17);
        map1.put("java", 25);
        System.out.println("map11"+map1);

        Map<String,Integer> map2=new HashMap();
        map2.put("张三丰", 100);
        map2.put("虚竹", 20);
        System.out.println("map2"+map2);
        //从指定映射种将所有的映射关系复制到此映射种
        map1.putAll(map2);
        System.out.println("map1"+map1);
    }
}
/* out
map11{java=25, rose=18, lucy=17, jack=20}
map2{张三丰=100, 虚竹=20}
map1{java=25, 张三丰=100, rose=18, lucy=17, jack=20, 虚竹=20}
*/
```

删除：

```java
package Set;

import java.util.HashMap;
import java.util.Map;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 13:48 2020/5/9
 */
public class Demo7 {
    public static void main(String[] args) {
        Map<String, Integer> map1 = new HashMap<>();
        map1.put("jack", 20);
        map1.put("rose", 18);
        map1.put("lucy", 17);
        map1.put("java", 25);
        System.out.println(map1);
        System.out.println("delete value:"+map1.remove("java"));
        map1.clear();
        System.out.println("map1"+map1);
    }
}
/* out
{java=25, rose=18, lucy=17, jack=20}
delete value:25
map1{}
*/
```

获取：

```java
package Set;

import java.util.HashMap;
import java.util.Map;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 13:48 2020/5/9
 */
public class Demo7 {
    public static void main(String[] args) {
        Map<String, Integer> map1 = new HashMap<>();
        map1.put("jack", 20);
        map1.put("rose", 18);
        map1.put("lucy", 17);
        map1.put("java", 25);
        System.out.println(map1);
        System.out.println("value:"+map1.get("jack"));
        System.out.println("map.size:"+map1.size());

    }
}
/* out
{java=25, rose=18, lucy=17, jack=20}
value:20
map.size:4
*/

```

判断：

```java
package Set;

import java.util.HashMap;
import java.util.Map;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 13:48 2020/5/9
 */
public class Demo7 {
    public static void main(String[] args) {
        Map<String, Integer> map1 = new HashMap<>();
        map1.put("jack", 20);
        map1.put("rose", 18);
        map1.put("lucy", 17);
        map1.put("java", 25);
        System.out.println(map1);
        System.out.println("isEmpty"+map1.isEmpty());
        System.out.println("containskey"+map1.containsKey("jack"));
        System.out.println("containsvaluse"+map1.containsValue(100));
    }
}
/* out
{java=25, rose=18, lucy=17, jack=20}
isEmptyfalse
containskeytrue
containsvalusefalse
*/
```

### 三.遍历Map的方式

- **使用KeySet**

  ```java
  package Set;
  
  import java.util.HashMap;
  import java.util.Iterator;
  import java.util.Map;
  import java.util.Set;
  
  /**
   * This program demonstrates
   *
   * @author Alita Alice
   * @version 1.0
   * @Date: Created in 13:48 2020/5/9
   */
  public class Demo7 {
      public static void main(String[] args) {
          Map<String, Integer> map1 = new HashMap<>();
          map1.put("jack", 20);
          map1.put("rose", 18);
          map1.put("lucy", 17);
          map1.put("java", 25);
          System.out.println(map1);
          Set<String> ks=map1.keySet();
          Iterator<String> it=ks.iterator();
          while (it.hasNext())
          {
              String key=it.next();
              Integer value = map1.get(key);
              System.out.println("key="+key+" value="+value);
          }
      }
  }
  /* out
  {java=25, rose=18, lucy=17, jack=20}
  key=java value=25
  key=rose value=18
  key=lucy value=17
  key=jack value=20
  */
  ```

  将Map转换成Set集合，通过Set的迭代器取出Set集合中的每一个元素（Iterator)就是Map集合中所有的键，再通过get方法获取键对应的值。

- 通过values获取所有的值，不能获取到key对象

  Collection<V> values()

  ```java
  public class Demo7 {
      public static void main(String[] args) {
          Map<String, Integer> map1 = new HashMap<>();
          map1.put("jack", 20);
          map1.put("rose", 18);
          map1.put("lucy", 17);
          map1.put("java", 25);
          Collection<Integer> vs=map1.values();  //values方法获取所有的值但是不能获取到KEY对象。
          Iterator<Integer> it = vs.iterator();
          while (it.hasNext())
          {
              Integer value=it.next();
              System.out.println("valuse=" +value);
          }
      }
  }
  ```

- Map.Entry

  面向对象的思想将Map集合中的键和值映射关系打包成一个对象，就是Map.Entry

  将该对象存入Set集合，Map.Entry是一个对象，那么该对象具备的getKey ，getValue获得键和值。（**通过Map中的entrySet()方法获取存放Map.Entry<K,V>对象的Set集合**。

  ```java
  public class Demo7 {
      public static void main(String[] args) {
          Map<Integer,String> map=new HashMap<>();
          map.put(1,"aaaa");
          map.put(2,"bbb");
          map.put(3, "cccc");
          System.out.println(map);
  
          Set<Map.Entry<Integer,String>> es=map.entrySet();
          Iterator<Map.Entry<Integer,String>> it=es.iterator();
          while (it.hasNext())
          {
              Map.Entry<Integer,String> en =it.next();
              Integer key=en.getKey();
              String value=en.getValue();
              System.out.println("key="+key+"value="+value);
          }
      }
  }
  /* out
  {1=aaaa, 2=bbb, 3=cccc}
  key=1value=aaaa
  key=2value=bbb
  key=3value=cccc
  */
  ```

## HashMap

底层是哈希表数据结构，线程是不同步的，**可以存入null键。**

要保证键的唯一性，需要覆盖hashCode方法 和equals方法

```java
package Set;

import java.util.*;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 22:09 2020/5/10
 */
public class Demo1 {
    public static void main(String[] args) {
        HashMap<Person,String> hm=new HashMap<>();
        hm.put(new Person("jack", 20), "1001");
        hm.put(new Person("rose", 18), "1002");
        hm.put(new Person("lucy", 19), "1003");
        hm.put(new Person("hmm", 17), "1004");
        hm.put(new Person("ll", 17), "1005");
        System.out.println(hm);
        System.out.println(hm.put(new Person("rose", 18), "1006"));
        Set<Map.Entry<Person,String>> entrySet =hm.entrySet();
        Iterator<Map.Entry<Person,String>> it= entrySet.iterator();
        while  (it.hasNext())
        {
            Map.Entry<Person,String> next=it.next();
            Person key =next.getKey();
            String value=next.getValue();
            System.out.println(key+ "=" +value);
        }

    }
}
class Person
{
    private  String name;
    private  int age;
    Person()
    {

    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person person = (Person) o;
        return getAge() == person.getAge() &&
                getName().equals(person.getName());
    }

    @Override
    public int hashCode() {
        return Objects.hash(getName(), getAge());
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
/* out 
{Person{name='ll', age=17}=1005, Person{name='jack', age=20}=1001, Person{name='hmm', age=17}=1004, Person{name='lucy', age=19}=1003, Person{name='rose', age=18}=1002}
1002
Person{name='ll', age=17}=1005
Person{name='jack', age=20}=1001
Person{name='hmm', age=17}=1004
Person{name='lucy', age=19}=1003
Person{name='rose', age=18}=1006
*/
```

## TreeMap

TreeMap的排序，TreeMap 可以对集合中的键进行排序，如何实现对键的排序？

### 方式1： 元素自身具备比较性

和TreeSet一样原理，需要让存储在键位置的对象实现Comparable接口。重写compareTo方法，也就是让元素自身具备比较性，这种方式叫做元素的自然排序也叫默认排序。

### 方式2：容器具备比较性

当元素自身不具备比较性，或者自身具备的比较性不是所需要的，那么此时可以让**容器自身具备**，需要定义一个类**实现接口Compatator，重写compare方法，并将该接口的子类实例对象作为参数传递给TreeMap集合的构造方法。**

注意：当Comparable比较方式和Comparator比较方式同时存在时，以Comparator的比较方式为主。

```java
package Set;

import java.util.*;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 22:09 2020/5/10
 */
public class Demo1 {
    public static void main(String[] args) {
       TreeMap<String,Integer> tree=new TreeMap<>();
        tree.put("张三",19);
        tree.put("李四",20);
        tree.put("王五",21);
        tree.put("赵留",21);
        System.out.println(tree);
        System.out.println("张三".compareTo("李四"));
    }
}
```

自定义元素排序

```java
package Set;

import java.util.*;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 22:09 2020/5/10
 */
public class Demo1 {
    public static void main(String[] args) {
     TreeMap<Person,String> hm=new TreeMap<Person, String>(new MyComparator());//该接口的子类实例对象作为参数传递给TreeMap集合的构造方法。
        hm.put(new Person("jack",20),"1001");
        hm.put(new Person("rose", 18), "1002");
        hm.put(new Person("lucy", 19), "1003");
        hm.put(new Person("hmm", 17), "1004");
        System.out.println(hm);


        Set<Map.Entry<Person,String>> entrySet=hm.entrySet();
        Iterator<Map.Entry<Person,String>> it=entrySet.iterator();
        while  (it.hasNext())
        {
            Map.Entry<Person,String> next=it.next();
            Person key=next.getKey();
            String value=next.getValue();
            System.out.println(key+ "=" +value);
        }
    }
}
class MyComparator implements Comparator<Person>
{

    @Override
    public int compare(Person p1,Person p2) {
        if(p1.getAge()>p2.getAge())
        {
            return -1;
        }
        if(p1.getAge()<p2.getAge())
        {
            return 1;
        }
        return p1.getName().compareTo(p2.getName());
    }
}
class Person implements Comparable<Person>
{
  private String name;
  private int age;
  Person(){}

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person person = (Person) o;
        return getAge() == person.getAge() &&
                getName().equals(person.getName());
    }

    @Override
    public int hashCode() {
        return Objects.hash(getName(), getAge());
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    @Override
    public int compareTo(Person p) {
      if(this.age>p.age) {
          return 1;
      }else if (this.age<p.age)
      {
          return -1;
      }
        return this.name.compareTo(p.name);
    }
}
/* out
{Person{name='jack', age=20}=1001, Person{name='lucy', age=19}=1003, Person{name='rose', age=18}=1002, Person{name='hmm', age=17}=1004}
Person{name='jack', age=20}=1001
Person{name='lucy', age=19}=1003
Person{name='rose', age=18}=1002
Person{name='hmm', age=17}=1004
*/
```

注意：Set元素不可重复，Map的键不可重复

​           如果存入重复元素如何处理?

Set元素重复元素不能存入add方法，返回false;

Map的重复键将覆盖旧键，将旧值返回。