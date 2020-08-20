---
title: ArrayList源码粗略解读（面试必问）
copyright: true
date: 2020-04-03 15:05:53
tags: ArrayList源码
categories: 源码解读
---

## 前言

> 现如今的Java程序员越来越多，学习者也越来越多。基本上使用Java的都会使用过HashSet、HashMap、ArrayList、LinkedList等集合，今天god-jiang就从源码层面上粗略解读一下ArrayList这个常用集合。

<!--more-->

**若是有写得不好的地方或者有错误，请读者提出，毕竟我也是一名菜鸡。**

## **1、ArrayList的介绍**

> ArrayList是一个容量能够动态增长的动态数组。但是它和数组又不一样，它继承了AbstractList，实现了List、RandomAccess（随机访问）、Cloneable、Serializable接口。

## **2、ArrayList的构造函数**

在JDK1.8的版本下，ArrayList有三个构造函数。分别是：

- **ArrayList()：构造一个初始容量为10的空数组列表**
- **ArrayList(int initialCapacity)：构造一个具有初始容量值的空数组列表**
- **ArrayList(Collection c)：构造一个包含指定元素的数组列表**

源码如下：

![img](https://pic3.zhimg.com/80/v2-cd48d01d46cf3a8ce129171ee05b00aa_720w.jpg)

![img](https://pic1.zhimg.com/80/v2-42b7ac5482c43ead09737c876d7734d0_720w.jpg)



![img](https://pic2.zhimg.com/80/v2-34ef99c6f234e0110c254409a8382fd9_720w.jpg)

## 3、ArrayList的add操作

在JDK1.8的版本里，add操作有两种，一种是按顺序一直添加，另一种是给定一个位置再添加。源码如下：

![img](https://pic1.zhimg.com/80/v2-c961c7f58cf634a486a60381836a241c_720w.jpg)

![img](https://pic4.zhimg.com/80/v2-b0a808405c6ac2a81171ddc0aed854ab_720w.jpg)

**就是进行add操作的时候，需要先进行ensureCapacityInternal操作，就是size+1判断是否需要扩容了，如果不需要，则直接插入，然后size++。如果需要扩容，就会扩容到原来的1.5倍，源码如下：**

![img](https://pic1.zhimg.com/80/v2-ae2bc676b0d1b2eadaa08c8bb9082128_720w.jpg)

## 4、ArrayList的遍历方式

给出ArrayList遍历常用的三种方式：

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

/**
 * @author god-jiang
 * @date 2020/4/3  14:22
 */
public class ArrayList_Resource {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("李白");
        list.add("露娜");
        list.add("韩信");

        //1、迭代器
        Iterator<String> it = list.iterator();
        while (it.hasNext()) {
            System.out.println(it.next());
        }
        System.out.println("================");

        //2、for
        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
        System.out.println("================");

        //3、for-each
        for (String str : list) {
            System.out.println(str);
        }
    }
}
```

肯定会有人问用哪个比较好，这里我只能说**博主经常使用的是第二种遍历方式，因为效率最高**。为啥效率最高，可以自己加入系统时间算时间差来比较得出。

## 5、ArrayList和LinkedList的区别（面试常问）

1. **是否保证线程安全**：ArrayList和LinkedList都是不同步的，也就是不保证线程安全；
2. **底层数据结构**：ArrayList底层使用的是Object数组；LinkedList底层使用的是双向链表；
3. **插入和删除是否受元素位置影响**：ArrayList采用数组存储，所以插入和删除元素的时间复杂度受元素的位置影响，为O(N)。LinkedList采用链表存储，所以插入和删除元素的时间复杂度不受元素位置的影响，为O(1)；
4. **是否支持快速随机访问**：LinkedList不支持高速的随机元素访问，而ArrayList支持；
5. **内存空间占用**：ArrayList的空间浪费主要体现在List列表的结尾会预留一定的容量空间，而LinkedList得空间花费体现在它得每一个元素都需要消耗比ArrayList更多的空间（因为要存放直接前驱和后继以及数据等）。

## 总结

> 今天的ArrayList源码就讲这么多，还有一些remove操作和contains操作我就没有写出来，不是说它们不重要，而是我把相对重要和常问的点拿出来讲一下。对ArrayList其他操作感兴趣可以自己看看源码，这个东西对你只会有好处而不会有坏处。

**谢谢大家，有错误或者写得不好的欢迎评论区评论或者私聊。**