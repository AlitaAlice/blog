---
title: Set相关
date: 2020-05-08 20:04:00
tags: JAVA集合
categories: JAVA集合

---

## 概述

> 本章介绍Set

<!--more-->

## 正文

## Set

**SET:注重独一无二的性质，该体系集合知道某物是否已经存在于集合中，不会存储重复的元素。**

用于存储无序（存入和取出的顺序不一定相同）元素，值不能重复

Set集合继承了Collection接口。

## HashSet

哈希表里面存放的是哈希值。HashSet存储元素的顺序并不是按照存入时的顺序（和List 显然不同）是按照哈希值来存，所以取也是按照哈希值来取得。

**元素的哈希值是通过元素的hashcode方法来获取的，HashSet首先判断俩个元素的哈希值，如果哈希值一样，那么接着比较equals方法，如果equals结果为true。HashSet就会视作同一个元素。如果equals为false 就不是同一个元素。**

### HashSet到底是如何判断俩个元素重复

通过hashCode方法和equals方法来保证元素的唯一性，add()返回的是boolean类型

判断两个元素是否相同，先要判断元素的hashCode值是否一致，只有在该值一致的情况下，才会判断equals方法，如果存储在HashSet中的两个对象hashCode方法的值相同equals方法返回的结果是true，那么HashSet认为这两个元素是相同元素，只存储一个（重复元素无法存入）。

注意：HashSet集合在判断元素是否相同先判断hashCode方法，如果相同才会判断equals。如果不相同，是不会调用equals方法的。

### HashSet 和ArrayList集合都有判断元素是否相同的方法

boolean contains(Object o)

HashSet使用hashCode和equals方法，ArrayList使用了equals方法

示例：

```java
public class Demo1 {
    public static void main(String[] args) {
        Set hs=new HashSet<>();
        hs.add("jack");
        hs.add("rose");
        hs.add("2020");
        hs.add("trip");
        System.out.println(hs.size());
        boolean add=hs.add("jack"); /* 如果set尚未包含指定元素，那么 返回true 此时返回false; */
        System.out.println(add);
        Iterator it=hs.iterator();
        while (it.hasNext())
        {
            System.out.println(it.next());
        }
    }
}
```


```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Objects;
import java.util.Set;

/**
 * This program demonstrates
 *
 * @author Alita Alice
 * @version 1.0
 * @Date: Created in 21:13 2020/5/8
 */
public class Demo1 {
    public static void main(String[] args) {
        HashSet hs = new HashSet();
        hs.add(new Person("jack", 20));
        hs.add(new Person("rose",20));
        hs.add(new Person("rose",20));
        Iterator it= hs.iterator();
        while(it.hasNext())
        {
            System.out.println(it.next());
        }

    }
}
class Person {
    private String name;
    private int age;

    Person(){

    }
    public Person(String name,int age)
    {
        this.age=age;
        this.name=name;
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



```

**其中在HashSet中存储自定义的对象，并尝试添加重复元素，需要override hashCode()和equals()方法。**

## TreeSet

现在有一批数据，要求不能重复存储元素，而且要排序。

ArrayList ，LinkList不能去除重复数据，HashSet可以去除重复，但是无序。

示例：使用TreeSet集合存储字符串元素，并且遍历。

```java
public class Demo5 {
    public static void main(String[] args) {
        TreeSet treeSet=new TreeSet();
        treeSet.add("aaa");
        treeSet.add("bbb");
        treeSet.add("ccc");
        treeSet.add("ddd");
        System.out.println(treeSet);
    }
}
/* 输出
[aaa, bbb, ccc, ddd]
*/
```

### 俩种比较器接口

```java
Comparable 
         compareTo(Object o)  元素自身具备比较性
Comparator
         compare(Object o1,Object o2) 给容器传入比较器
```

### TreeSet集合排序的俩种方式

- 让元素自身具备比较性

  元素需要实现Comparable接口，覆盖compareTo(Object o) 方法

  这种方式也被称为元素的自然排序，也可以称为默认排序

  年龄按照首要条件，年龄相同再比姓名

  ```java
  package Set;
  
  import sun.reflect.generics.tree.Tree;
  
  import java.util.Objects;
  import java.util.TreeSet;
  
  /**
   * This program demonstrates
   *
   * @author Alita Alice
   * @version 1.0
   * @Date: Created in 10:23 2020/5/9
   */
  public class Demo4 {
      public static void main(String[] args) {
          TreeSet ts=new TreeSet();
          ts.add(new Person("aa", 20, "男"));
          ts.add(new Person("bb", 18, "女"));
          ts.add(new Person("cc", 17, "男"));
          ts.add(new Person("dd", 17, "女"));
          ts.add(new Person("dd", 15, "女"));
          ts.add(new Person("dd", 15, "女"));
          System.out.println(ts);
          System.out.println(ts.size());
      }
  }
   class Person implements Comparable
   {
       private String name;
       private int age;
       private String gender;
  
       public Person(String name, int age, String gender) {
           this.name = name;
           this.age = age;
           this.gender = gender;
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
  
       public String getGender() {
           return gender;
       }
  
       public void setGender(String gender) {
           this.gender = gender;
       }
  
       @Override
       public String toString() {
           return "Person{" +
                   "name='" + name + '\'' +
                   ", age=" + age +
                   ", gender='" + gender + '\'' +
                   '}';
       }
  
       @Override
       public boolean equals(Object o) {
           if (this == o) return true;
           if (!(o instanceof Person)) return false;
           Person person = (Person) o;
           return getAge() == person.getAge() &&
                   getName().equals(person.getName()) &&
                   getGender().equals(person.getGender());
       }
  
       @Override
       public int hashCode() {
           return Objects.hash(getName(), getAge(), getGender());
       }
  
       @Override
       public int compareTo(Object o) {
           Person p = (Person) o;
           System.out.println(this + "compareTo:" + p);
           if (this.age > p.age) {
               return 1;
           }
           if (this.age < p.age) {
               return -1;
           }
           return this.name.compareTo(p.name);
       }
   }
  /* out
  Person{name='aa', age=20, gender='男'}compareTo:Person{name='aa', age=20, gender='男'}
  Person{name='bb', age=18, gender='女'}compareTo:Person{name='aa', age=20, gender='男'}
  Person{name='cc', age=17, gender='男'}compareTo:Person{name='aa', age=20, gender='男'}
  Person{name='cc', age=17, gender='男'}compareTo:Person{name='bb', age=18, gender='女'}
  Person{name='dd', age=17, gender='女'}compareTo:Person{name='bb', age=18, gender='女'}
  Person{name='dd', age=17, gender='女'}compareTo:Person{name='cc', age=17, gender='男'}
  Person{name='dd', age=15, gender='女'}compareTo:Person{name='bb', age=18, gender='女'}
  Person{name='dd', age=15, gender='女'}compareTo:Person{name='cc', age=17, gender='男'}
  Person{name='dd', age=15, gender='女'}compareTo:Person{name='bb', age=18, gender='女'}
  Person{name='dd', age=15, gender='女'}compareTo:Person{name='cc', age=17, gender='男'}
  Person{name='dd', age=15, gender='女'}compareTo:Person{name='dd', age=15, gender='女'}
  [Person{name='dd', age=15, gender='女'}, Person{name='cc', age=17, gender='男'}, Person{name='dd', age=17, gender='女'}, Person{name='bb', age=18, gender='女'}, Person{name='aa', age=20, gender='男'}]
  */
  ```

  ### 二 让容器自身具备比较性，自定义比较器

  需求：当元素自身不具备比较性，或者元素自身具备的比较性不是所需。

  **那么这时只能让容器自身具备定义一个类实现Comparetor接口，覆盖compare方法**

  **并将该接口的子类对象作为参数传递给TreeSet集合的构造函数。**

  当Comparable 比较方式及Comparator比较方式同时存在， 以Comparator比较方式为主。

  ```java
package Set;
  import java.util.Comparator;
  import java.util.Objects;
  import java.util.TreeSet;
  
  /**
   * This program demonstrates
   *
   * @author Alita Alice
   * @version 1.0
   * @Date: Created in 10:54 2020/5/9
   */
  public class Demo6 {
      public static void main(String[] args) {
          TreeSet ts=new TreeSet(new MyComparator());
          ts.add(new Book("think in java", 100));
          ts.add(new Book("java 核心技术", 75));
          ts.add(new Book("现代操作系统", 50));
          ts.add(new Book("java就业教程", 35));
          ts.add(new Book("think in java", 100));
          ts.add(new Book("ccc in java", 100));
  
          System.out.println(ts);
      }
  
  }
  class MyComparator implements Comparator
  {
      @Override
      public int compare(Object o1, Object o2) {
                      Book b1=(Book) o1;
                      Book b2=(Book) o2;
          System.out.println(b1+"comparator"+b2);
          if(b1.getPrice()>b2.getPrice())
          {
              return 1;
          }
          if(b1.getPrice()<b2.getPrice())
          {
              return -1;
          }
          return b1.getName().compareTo(b2.getName());
      }
  }
  class Book
  {
      private String name;
      private double price;
  
      public Book() {
      }
  
      public String getName() {
          return name;
      }
  
      public Book(String name, double price) {
          this.name = name;
          this.price = price;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public double getPrice() {
          return price;
      }
  
      public void setPrice(double price) {
          this.price = price;
      }
  
      @Override
      public boolean equals(Object o) {
          if (this == o) return true;
          if (!(o instanceof Book)) return false;
          Book book = (Book) o;
          return Double.compare(book.getPrice(), getPrice()) == 0 &&
                  getName().equals(book.getName());
      }
  
      @Override
      public int hashCode() {
          return Objects.hash(getName(), getPrice());
      }
  
      @Override
      public String toString() {
          return "Book{" +
                  "name='" + name + '\'' +
                  ", price=" + price +
                  '}';
      }
  }
  /* out
  Book{name='think in java', price=100.0}comparatorBook{name='think in java', price=100.0}
  Book{name='java 核心技术', price=75.0}comparatorBook{name='think in java', price=100.0}
  Book{name='现代操作系统', price=50.0}comparatorBook{name='think in java', price=100.0}
  Book{name='现代操作系统', price=50.0}comparatorBook{name='java 核心技术', price=75.0}
  Book{name='java就业教程', price=35.0}comparatorBook{name='java 核心技术', price=75.0}
  Book{name='java就业教程', price=35.0}comparatorBook{name='现代操作系统', price=50.0}
  Book{name='think in java', price=100.0}comparatorBook{name='java 核心技术', price=75.0}
  Book{name='think in java', price=100.0}comparatorBook{name='think in java', price=100.0}
  Book{name='ccc in java', price=100.0}comparatorBook{name='java 核心技术', price=75.0}
  Book{name='ccc in java', price=100.0}comparatorBook{name='think in java', price=100.0}
  [Book{name='java就业教程', price=35.0}, Book{name='现代操作系统', price=50.0}, Book{name='java 核心技术', price=75.0}, Book{name='ccc in java', price=100.0}, Book{name='think in java', price=100.0}]
  */
  
  ```
  
  ### 4.LinkedHashSet
  

LinkedHashSet会保存插入的顺序

看到array，就要想到角标

看到link ，就要想到first,last

看到hash,就要想到hashCode，equals

看到tree，就要想到俩个接口。Comparable,Comparator 

###       5.set为什么是不允许重复的

现在我们就从 Set 说起。

Set 接口为我们提供了一个 add() 方法，以让我们添加元素。所以我们看一下在其实现类 HashSet 中是如何实现的呢？

我们看 HashSet 中的 add() 方法实现；

  public boolean add( E o ) {

​       return ***\*map.put(o, PRESENT)==null;\****

}

你可能回问怎么回出来 map 了呢？

Map 又是一个什么变量呢？

我们来看 map 是在在哪定义的。原来，在 HashSet 中定义了这样的两个变量：

  private transient HashMap<E,Object> map;

  private static final Object PRESENT = new Object();

我们再看一下上面的 add() 方法。

map.put(o, PRESENT)==null

实际执行的是 map 的方法，并且我们添加的对象是 map 中的 key,value 是执行的同一个对象PRESENT.

***\*因为map中的key是不允许重复的，所以set中的元素不能重复。\****