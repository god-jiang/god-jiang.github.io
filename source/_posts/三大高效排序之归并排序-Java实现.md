---
title: 三大高效排序之归并排序(Java实现)
date: 2019-12-16 20:38:21
tags: 高效排序
categories: 算法积累ing
---

## 归并排序的介绍

归并排序(英语：Merge sort，或Mergesort)，是创建在归并操作上的一种有效的排序算法，效率为O(n log n)。1945年由约翰·冯·诺伊曼首次提出。该算法是采用分治法（Divide and Conquer）的一个非常典型的应用，且各层分治递归可以同时进行。

<!--more-->

## 概念

是利用递归与分治的技术将数据序列划分为越来越小的半子表，再对半子表排序，最后再用递归方法将排好序的半子表合并成越来越大的有序序列。

## 核心思想

**将两个有序的数列合并成一个大的有序的序列。通过递归，层层合并，即为归并。**

![](/images/归并排序图示.png)

## 实现代码

```java
import java.util.Arrays;

//归并排序，时间复杂度为O(N*logN)，空间复杂度为O(N)
public class MergeSort {
    public static void MergeSort(int[] arr, int start, int end) {
        //分治的结束条件
        if (start >= end) {
            return;
        }
        //保证不溢出取start和end的中位数
        int mid = start + ((end - start) >> 1);
        //递归排序并且合并
        MergeSort(arr, start, mid);
        MergeSort(arr, mid + 1, end);
        Merge(arr, start, mid, end);
    }

    //合并
    public static void Merge(int[] arr, int start, int mid, int end) {
        int[] temp = new int[end - start + 1];
        int p1 = start;
        int p2 = mid + 1;
        int p = 0;
        while (p1 <= mid && p2 <= end) {
            if (arr[p1] > arr[p2]) {
                temp[p++] = arr[p2++];
            } else {
                temp[p++] = arr[p1++];
            }
        }
        while (p1 <= mid) {
            temp[p++] = arr[p1++];
        }
        while (p2 <= end) {
            temp[p++] = arr[p2++];
        }
        for (int i = 0; i < temp.length; i++) {
            arr[i + start] = temp[i];
        }
    }

    public static void main(String[] args) {
        int[] a = {2, 4, 6, 1, 3, 7, 9, 8, 5};
        MergeSort(a, 0, a.length - 1);
        System.out.println(Arrays.toString(a));
    }
}

```

## 运行截图

![](/images/归并运行截图.png)

> 1、以上就是今天分享的归并排序，时间复杂度为O(N*logN)，空间复杂度为O(N)
>
> 2、归并排序的额外空间复杂度可以做到O(1)，但是非常难，不需要掌握，有一篇论文"归并排序内部缓存法"可以做到