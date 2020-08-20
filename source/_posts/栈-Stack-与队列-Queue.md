---
title: 栈(Stack)与队列(Queue)
copyright: true
date: 2020-01-06 16:36:24
tags: 栈与队列
categories: 算法积累ing
---

## 定义

> 栈：后进先出（LIFO-last in first out）：最后插入的元素最先出来。
> 队列：先进先出（FIFO-first in first out）：最先插入的元素最先出来。

<!--more-->

## 图示

![img](/images/栈与队列/栈与队列.jpg)



**本文通过一些简单的算法题来带你们更好的理解栈(Stack)和队列(Queue)。**

## 三道算法题加深理解

### **第一题**

**题目：获取一个栈的min**

> **定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O(1)）。**

```java
import java.util.Stack;

/**
 * @author god-jiang
 * @date 2020/1/6
 */
public class Format3 {
    //正常stack
    Stack<Integer> stack = new Stack<>();
    //存放min的stack
    Stack<Integer> help = new Stack<>();

    public void push(int node) {
        stack.push(node);
        if (help.isEmpty()) {
            help.push(node);
        } else {
            //help里面存放的都是最小值,也就是pop之后里面是当前的最小值
            int res = help.peek() > node ? node : help.peek();
            help.push(res);
        }
    }

    public void pop() {
        stack.pop();
        help.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int min() {
        return help.peek();
    }
}
```

### 第二题

**题目：用栈实现队列**

**思路：构建两个栈（Push栈和Pop栈）;将Push栈中的数据导入Pop栈中然后返回给用户，就实现了队列。需要注意两个条件：①Pop栈为空时才能往里面倒数据。②向Pop栈倒数据必须全部倒完。**

```java
import java.util.Stack;

/**
 * @author god-jiang
 * @date 2020/1/6
 */
public class StackToQueue {
    //用s1、s2避免代码看起来混乱，因为都是push和pop操作
    private Stack<Integer> s1;
    private Stack<Integer> s2;

    public StackToQueue() {
        s1 = new Stack<>();
        s2 = new Stack<>();
    }

    public void add(int obj) {
        s1.push(obj);
    }

    public Integer poll() {
        if (s1.isEmpty() && s2.isEmpty()) {
            throw new RuntimeException("empty");
        }
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
        }
        return s2.pop();
    }

    public Integer peek() {
        if (s1.isEmpty() && s2.isEmpty()) {
            throw new RuntimeException("empty");
        }
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
        }
        return s2.peek();
    }
}
```

### 第三题

**题目：用队列实现栈**

**思路：构建两个队列：queue队列和help队列；压入数据时数据都进queue队列，假设队列中进入了1、2、3、4、5，返回数据时，把1、2、3、4放入help队列，然后拿出queue的5返回。接着把queue队列和help队列的引用交换。即下次返回数据还是从queue队列拿1、2、3、放入help队列，然后queue拿出4返回，再交换各自的引用，一直重复。**

```java
import java.util.LinkedList;
import java.util.Queue;

/**
 * @author god-jiang
 * @date 2020/1/6
 */
public class QueueToStack {
    private Queue<Integer> queue;
    private Queue<Integer> help;

    public QueueToStack() {
        queue = new LinkedList<>();
        help = new LinkedList<>();
    }

    public void push(Integer e) {
        queue.add(e);
    }

    public int pop() {
        if (queue.isEmpty()) {
            throw new RuntimeException("empty");
        }
        while (queue.size() != 1) {
            help.add(queue.poll());
        }
        int res = queue.poll();
        swap();
        return res;
    }

    public int peek() {
        if (queue.isEmpty()) {
            throw new RuntimeException("empty");
        }
        while (queue.size() != 1) {
            help.add(queue.poll());
        }
        int res = queue.poll();
        help.add(res);
        swap();
        return res;
    }

    public void swap() {
        Queue<Integer> tmp = queue;
        queue = help;
        help = tmp;
    }
}
```

## 总结

> 就是把栈跟队列的特点介绍了一下，然后用三道经典的题目来加深对栈和队列的理解，然后附上我自己写的代码，都是经过测试后才附上的。有什么问题，欢迎与我交流和讨论，我的目的就是大家一起学习一起进步。

