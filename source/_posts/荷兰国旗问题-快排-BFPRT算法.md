---
title: 荷兰国旗问题&快排&BFPRT算法
date: 2019-12-26 16:17:35
tags: 算法进阶
categories: 算法积累ing
---

## 荷兰国旗问题

> 给定一个数组arr和一个数num，请把小于num的数放在数组的左边，等于num的数放在数组的中间，大于num的数放在数组的右边。要求额外空间复杂度为O(1)，时间复杂度为O(N)

<!--more-->

### 解决思路

初始化less=-1，more=len(arr)，当前位置为cur=0。

- 如果arr[cur]<num，交换arr[cur]和arr[++less]的数，然后cur++
- 如果arr[cur]>num，交换arr[cur]和arr[--more]的数，然后cur不变
- 如果当前位置上的数等于num，less和more均不变，cur++
- 当cur==more时，停止比较，返回

### 代码

```java
public class NetherLandsFlag{
    public static int[] partition(int[] arr, int L, int R, int num) {
        int less = L - 1;//小于区域的边界
        int more = R + 1;//大于区域的边界
        int cur = 0;
        while (cur < more) {
            if (arr[cur] < num) {
                swap(arr, ++less, cur++);
            } else if (arr[cur] > num) {
                swap(arr, --more, cur);
            } else {
                cur++;
            }
        }
        return arr;
    }
    
    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    
    public static void main(String[] args){
        int[] arr = new int[]{7, 2, 9, 3, 5, 8, 8, 5, 1, 6, 6, 4};
        int[] res = partition(arr, 0, arr.length - 1, 5);
        System.out.println(Arrays.toString(res));
    }
}
```

### 运行截图

![](/images/荷兰国旗.png)

------



## 稳定算法的定义

> 假定在待排序的记录序列中，存在多个具有相同的关键字的记录，若经过排序，这些记录的相对次序保持不变，即在原序列中，r[i]=r[j]，且r[i]在r[j]之前，而在排序后的序列中，r[i]仍在r[j]之前，则称这个排序算法是稳定的；否则称为不稳定的。

------



## BFPRT算法

### 背景介绍

> 在一大堆数中求其前k大或前k小的问题，简称TOP-K问题。目前解决TOP-K问题最有效的算法是BFPRT算法，又称为中位数的中位数算法，该算法由Blum、Floyd、Pratt、Rivest、Tarjan提出，最坏时间复杂度为O(N)

一般第一反应解决TOP-K问题就是对所有数据进行一次排序，然后取其前k即可，但是有两个问题：

1. 排序的平均复杂度为O(n*logn)，最坏时间复杂度为O(n^2)，不能保证较好的复杂度
2. 我们只需要前k大的数，而对其余不需要的数也进行了排序，浪费了大量排序时间

除了这种方法之外，堆排序也是一个比较好的选择， 可以维护一个大小为k的堆，时间复杂度为O(n*logk)。

### 算法套路

1. 对整个数组进行分组，每组5个数，不满5个的凑成最后一组
2. 对每个组进行组内排序，组内5个数排序的时间复杂度为O(1)，所以总共有n/5个组，时间复杂度为O(N)
3. 拿出排序后的每个组的中位数，组成一个新的n/5长度的数组
4. 递归调用BFPRT算法，求出最后的中位数num
5. 拿到BFPRT的返回的num，利用荷兰国旗算法把小于的放在数组的左边，等于的放在数组的中间，大于放在数组的右边。

### 伪代码

```java
public class BFPRT{
	public int bfprt(int[] arr,int k){
        //1、对arr数组进行分组，每5个为一组
        //2、进行组内排序，时间复杂度为O(N)，取出每个组的中位数
        //3、每个组的中位数组成一个n/5的数组new_arr
        //4、递归bfprt(new_arr,new_arr.length/2)
        //5、得到一个中位数num
    }
    //利用这个中位数进行荷兰国旗算法，小于在左边，等于在中间，大于在右边
    //如果num==k,则该中位数就是第k大的数
    //如果num<k，则递归求num之后的数组
    //如果num>k，则递归求num之前的数组
}
```

### 时间复杂度证明

![](/images/BFPRT时间复杂度.png)

------



## 参考文献

1. 算法导论
2. csdn博客

> 以上讲的是荷兰国旗的解法，可以运用于经典快排算法的partition操作，也可以用于BFPRT算法求解（TOP-K问题）