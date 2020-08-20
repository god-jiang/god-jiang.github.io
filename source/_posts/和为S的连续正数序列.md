---
title: 和为S的连续正数序列
copyright: true
date: 2020-02-04 11:42:14
tags: 中等
categories: LeetCode&牛客题解
---

## 题目描述

> 小明很喜欢数学，有一天他在做数学作业时，要求计算出9~16的和，他马上就写出了正确答案是100。但是他并不满足于此，他在想究竟有多少种连续的正数序列的和为100（至少包括两个数）。没多久，他就得到另一组连续正数和为100的序列：18，19，20，21，22。现在把问题交给你，你能不能也很快的找到所有和为S的连续正数序列？Good Luck！

<!--more-->

## 输出描述

> 输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序

## 暴力思路

就是正常的暴力解法，穷举所有可能相加等于S，本文章不讲这个解法。

## 双指针思路

设置两个指针left和right，然后根据等差数列的求和公式（a0+an）* n / 2求出对应的和与S比较，等于的话直接返回；小于S的话就right++；大于S的话就left++。

## 代码

```java
package nowcoder;

import java.util.ArrayList;

/**
 * @author god-jiang
 * @date 2020/2/4  11:35
 */
public class FindContinuousSequence {
    public ArrayList<ArrayList<Integer>> findContinuousSequence(int sum) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        //设置两个指针left和right
        int left = 1;
        int right = 2;
        while (left < right) {
            //因为都是连续的，差值为1的等差数列。
            //求和公式为(a0+an)*n/2
            int curSum = (left + right) * (right - left + 1) / 2;
            //判断curSum和sum的大小关系调整对应的left和right
            if (curSum == sum) {
                ArrayList<Integer> list = new ArrayList<>();
                for (int i = left; i <= right; i++) {
                    list.add(i);
                }
                res.add(list);
                left++;
            } else if (curSum < sum) {
                right++;
            } else {
                left++;
            }
        }
        return res;
    }
}
```

## 通过截图

![img](https://pic4.zhimg.com/80/v2-a97efb8af8961a1eae45f96044881e87_hd.jpg)

## 总结

> 其实这道题我半年前就做过了，然后当时根本对算法没多少认识，基本都是一个思路“暴力破万法”，“一切皆可暴”。所以慢慢接触到一些面经，基本就是算法题你只要是暴力解的基本都是不通过，这就给我提了个醒，不能一直依靠暴力，暴力就当作入门，后面要多学习算法达到一道题有多种解法思路。