---
title: 三大高效排序之堆排序(Java实现)
date: 2019-12-17 13:17:22
tags: 高效排序
categories: 算法积累ing
---

## 堆排序的介绍

> 堆排序(Heapsort)是指利用堆积树（堆）这种数据结构所设计的一种排序算法，它是选择排序的一种。可以利用数组的特点快速定位指定索引的元素。堆分为大根堆和小根堆，是**完全二叉树**。

<!--more-->

- 完全二叉树：除了最后一层之外的其他每一层都被完全填充，每一层从左到右的填充数据，不能空缺
- 大根堆：任意一个节点的值均大于等于它的左右孩子的值，位于堆顶的节点值最大
- 小根堆：任意一个节点的值均小于等于它的左右孩子的值，位于堆顶的节点值最小

**本节分享的堆排序以大根堆为例子**

## 堆排序的实现步骤

- ### 把一个数组调整为大根堆（heapInsert）

  假设当前节点的下标为i，那么它的父亲节点为(i-1)/2，每次heapInsert的时候就把insert进来的节点与它的父亲节点进行比较，比它的父节点大就交换，一直重复调整

- ### 每次把堆顶放到最后的节点位置，然后调整整个堆为大根堆（heapify）

  每次把堆顶的节点放到最后，然后堆大小减1，然后调整为大根堆，一直重复，直到大根堆的大小为0为止



## 代码实现

```java
import java.util.Arrays;

//堆排序
public class HeapSort {
    public static void main(String[] args) {
        int[] arr = {3, 4, 5, 6, 7, 1, 2, 9, 8};
        int size = arr.length;
        for (int i = 0; i < size; i++) {
            heapInsert(arr, i);
        }
        swap(arr, 0, --size);
        while (size > 0) {
            heapify(arr, 0, size);
            swap(arr, 0, --size);
        }
        System.out.println(Arrays.toString(arr));
    }

    //heapInsert操作
    public static void heapInsert(int[] arr, int index) {
        while (arr[index] > arr[(index - 1) / 2]) {
            swap(arr, index, (index - 1) / 2);
            index = (index - 1) / 2;
        }
    }

    //heapify操作
    public static void heapify(int[] arr, int index, int size) {
        int left = 2 * index + 1;
        while (left < size) {
            int largest = left + 1 < size && arr[left + 1] > arr[left] ? left + 1 : left;
            largest = arr[index] > arr[largest] ? index : largest;
            if (largest == index)
                break;
            swap(arr, index, largest);
            index = largest;
            left = 2 * index + 1;
        }
    }
    
    //交换两数
    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}

```

## 运行截图

![](/images/归并运行截图.png)

> 以上就是今天分享的堆排序，主要操作是heapInsert和heapify，时间复杂度为O(N*logN)，空间复杂度为O(1)