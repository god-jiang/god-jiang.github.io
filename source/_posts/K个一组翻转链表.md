---
title: K个一组翻转链表
copyright: true
date: 2020-02-14 11:52:28
tags: 困难
categories: LeetCode&牛客题解
---

## 题目描述

> 给你一个链表，每k个节点一组进行翻转，请你返回翻转后得链表。
>
> k是一个正整数，它的值小于或等于链表的长度。
>
> 如果节点总数不是k的整数倍，那么请将最后剩余的节点保持原有顺寻。

<!--more-->

## 示例

> 给定这个链表：1->2->3->4->5
>
> 当k=2时，应当返回：2->1->4->3->5
>
> 当k=3时，应当返回：3->2->1->4->5

## 思路（看图看代码）

用4个指针（pre, end, start, next）来记录完成整个过程。

![img](https://pic4.zhimg.com/v2-7f54e75544b77687679355112c275ca3_b.png)

![img](https://pic1.zhimg.com/v2-b3bb4db2076ec2ce1b12ecd2ba96f170_b.png)

## 代码

```java
package leetcode;

/**
 * @author god-jiang
 * @date 2020/2/14  11:21
 */
public class ReverseKGroup {
    //定义链表
    public class ListNode {
        int val;
        ListNode next = null;

        ListNode(int val) {
            this.val = val;
        }
    }
    //K个一组翻转链表
    public ListNode reverseKGroup(ListNode head, int k) {
        //dummy是虚拟节点
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        ListNode end = dummy;
        while (end != null) {
            for (int i = 0; i < k && end != null; i++) {
                end = end.next;
            }
            if (end == null) {
                break;
            }
            ListNode start = pre.next;
            ListNode next = end.next;
            end.next = null;
            pre.next = reverse(start);
            start.next = next;
            pre = start;
            end = start;
        }
        return dummy.next;
    }

    //反转链表并返回头节点
    public ListNode reverse(ListNode head) {
        ListNode p1 = head;
        ListNode p2 = head.next;
        ListNode p3 = null;
        while (p2 != null) {
            p3 = p2.next;
            p2.next = p1;
            p1 = p2;
            p2 = p3;
        }
        head.next = null;
        head = p1;
        return head;
    }
}
```

## 复杂度分析

- 时间复杂度为O(N*K)。最好的情况是O(N)，最坏的情况是O(N^2)
- 空间复杂度为O(1)

**PS：这道题确实挺有难度，然后leetcode上我参考了王小二大佬的图和思路，然后自己写的代码。**