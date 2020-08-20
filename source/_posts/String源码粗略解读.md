---
title: String源码粗略解读
copyright: true
date: 2020-04-15 14:30:20
tags: String源码
categories: 源码解读
---

## 前言

> 基本上只要是Java程序员，就肯定会接触过String类。博主我是大三参加蓝桥杯比赛才学会用String类的charAt（），length（），toString（）等等常用函数。所以今天有时间来看看String的源码，分析一下我们常用的方法在源码层面是什么样子的。

<!--more-->

## String类

![img](https://pic1.zhimg.com/80/v2-c4d5017b5eeeda1d234b33e3da017b04_720w.jpg)

源码中String类是用final关键字修饰的，表示String类是一个不可变的类。然后String类实现了Serializable、Comparable、CharSequence接口。它们分别有什么作用呢？

1. **Serializable接口，表示这个类是能够被序列化的，便于在网络中传输和保存。**
2. **Comparable接口，里面只有一个compareTo方法，这个是用来进行排序的，如果返回-1，则当前对象排在前面；如果返回1，则当前对象排在后面；返回0，则表示相等。**
3. **CharSequence接口，里面就是定义一些常用的方法，如charAt（int），length（），toString（）等。**

## String的定义变量

![img](https://pic4.zhimg.com/80/v2-9f45b43bb6fd1e60e16ee6fb6d27c0db_720w.jpg)

从构造函数可以看出来，其实String类的底层是char类型的数组。然后String类还会把对应的hash值记录下来。这就是为什么HashMap比较喜欢用String类做为key的原因。因为String类会hashcode缓存下来，不用多一步计算它的hash值。

1. **value[]表示是String的底层用的是char类型的数组。**
2. **hash表示变量的hash值，用hash来记录下来。**
3. **serialVersionUID表示序列化机制，用来验证版本的一致性。**

## equal（Object）方法

![preview](https://pic3.zhimg.com/v2-5d66762b148bb1439243be8b7f72998e_r.jpg)

String类重写了equal（）方法，因为Object类原始的equal（）方法是“==”。String类的equal（）方法就是判断是不是同一个类型，如果是，则对比它们的长度，如果相等，则对比它们的字符。**简单来说，就是判断两个字符串的值是否一样。**

## hashCode（）方法

![img](https://pic2.zhimg.com/80/v2-2feee68934700e449dbb4ca937f344d1_720w.jpg)

String类的hashCode（）方法就是hash值乘以31然后加每位的值。然而即使你的hash函数设计得再好，也是会产生hash碰撞。**所以一般两个字符串的hashcode相等并不代表它们相等，还需要判断它们是否equal（）相等才可以。**

## toString（）方法

![img](https://pic1.zhimg.com/80/v2-79f25f4860dfea33718aace9245b04c4_720w.jpg)

![preview](https://pic3.zhimg.com/v2-0de4c1c509999dbe8fcdc415187164ea_r.jpg)

toString（）用的就是Object类的toString（）方法。**就是返回一个类名+@+hashCode的16进制的数字的字符串。**

## intern（）方法

![img](https://pic1.zhimg.com/80/v2-7706884725439c846330a7f0e9203b84_720w.jpg)

String类的intern（）方法是native的。就是本地方法，**该方法的实现由非Java语言实现，比如C、C++。这个特征并非Java所持有，很多其它的编程语言都有这一个机制。**

**intern（）方法的用途是当前的字符对象（通过new出来的对象）可以使用intern方法从常量池中获取，如果常量池中不存在该字符串，那么就会新建一个新的字符串放到常量池中。**

```java
/**
 * @author god-jiang
 * @date 2020/4/15  14:22
 */
public class Main {
    public static void main(String[] args) {
        String str1 = "god-jiang";
        String str2 = new String("god-jiang");
        String str3 = new String("god-jiang").intern();

        System.out.println(str1 == str2); //false
        System.out.println(str1 == str3); //true
    }
}
```

## 总结

> String类还是有很多常用的函数我没有全部说到，比如isEmpty（），indexOf（），substring（），concat（）等等。我就写了一些比较浅的源码解读，其他的方法也写得很不错，如果你们感兴趣可以多去看看源码，这样可以增加你的知识。