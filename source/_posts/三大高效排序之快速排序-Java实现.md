---
title: 三大高效排序之快速排序(Java实现)
date: 2019-12-16 12:33:10
tags: 高效排序
categories: 算法积累ing
---

## 概念

快速排序是一种原地排序，只需要一个很小的栈作为辅助空间，空间复杂度为O(logN)，所以适合在数据集比较大且无序的时候使用。

**时间复杂度**

时间复杂度比较复杂，最好的情况是O(N)，最差的时候是O(N^2)，所以平时说的O(N*logN)为其平均时间复杂度。

<!--more-->

## 基本思想

随机找出一个数，可以随机取，也可以取固定位置，一般是取第一个或最后一个称为基准，然后就是比基准小的在左边，比基准大的放到右边，如何放做，就是和基准进行交换，这样交换完左边都是比基准小的，右边都是比较基准大的，这样就将一个数组分成了两个子数组，然后再按照同样的方法把子数组再分成更小的子数组，直到不能分解为止。

## 操作实现

partition方法中

1.选择数组中的第一个元素arr[startIndex]作为轴（pivot）

2.左指针为left，从最左边开始寻找第一个比pivot大的数

3.右指针为right，从最右面的一个元素开始向左寻找第一个小于等于pivot的数值

4.经过2，3两个步骤后，将会出现以下两种情况

​           （1）：left和right没有相遇，此时进行交换，swap（arr,left,right）;

​           （2）：left和right相遇，做swap（arr,startIndex,left），然后返回left

5.partition中返回pivot用于分割数组，下一次用于排序的数组被分割为(startIndex,pivot-1),(pivot+1,endIndex)两段，进行递归操作

## 代码实现

```java
import java.util.Arrays;
public class QuickSort {
    public static void main(String[] args) {
        int[] a = {2, 4, 6, 1, 3, 7, 9, 8, 5};
        quickSort(a, 0, a.length - 1);
        System.out.println(Arrays.toString(a));
    }

    //时间复杂度O(n*logn)，空间复杂度O(n*logn)
    public static void quickSort(int[] arr, int startIndex, int endIndex) {
        if (startIndex < endIndex) {
            //找出基准
            int partition = partition(arr, startIndex, endIndex);
            //分成两边递归进行
            quickSort(arr, startIndex, partition - 1);
            quickSort(arr, partition + 1, endIndex);
        }
    }

    //找基准
    private static int partition(int[] arr, int startIndex, int endIndex) {
        int pivot = arr[startIndex];
        int left = startIndex;
        int right = endIndex;
        while (left != right) {
            while (left < right && arr[right] > pivot) {
                right--;
            }
            while (left < right && arr[left] <= pivot) {
                left++;
            }
            //找到left比基准大，right比基准小，进行交换
            if (left < right) {
                swap(arr, left, right);
            }
        }
        //第一轮完成，让left和right重合的位置和基准交换，返回基准的位置
        swap(arr, startIndex, left);
        return left;
    }

    //两数交换
    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```

## 运行截图

![](/images/快排运行截图.png)

> 1、以上就是今天分享的快速排序，时间复杂度为O(N*logN)，空间复杂度为O(N\*logN)
>
> 2、快排是不稳定排序，要想做到稳定性是可以的，但是非常难，不需要掌握，有一篇论文叫"01 stable sort"可以做到
>
> 3、有一道题目，是奇数放数组左边，偶数放在数组右边，还要求原始的相对次序不变，额外空间复杂度为O(1)，碰到这个问题，直接可以怼面试官，根本不可能做出来

