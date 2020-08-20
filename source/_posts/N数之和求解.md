---
title: N数之和求解
copyright: true
date: 2020-01-24 18:56:09
tags: 中等
categories: LeetCode&牛客题解
---

## 背景

> 刷leetcode上的题发现有一些题型相似的题目可以单独拿出来一起练习，因为相似，所以可以用同一种解法优化一下就可以做，以达到巩固的效果，本文就把介绍**两数之和（简单）**和**三数之和（中等）**的解法，类似的四数之和等等都是类似的。

<!--more-->

## 题目1描述（两数之和）

![img](/images/N数之和/1.jpg)

## 解题思路

> 利用**哈希表**来解题，利用“空间换时间”。把**nums[i]的值作为哈希表的key**，把 **i 作为哈希表的value**。然后**判断target-nums[i]是否在哈希表中出现过**就可以找到了。

## 代码

```java
package leetcode;

import java.util.HashMap;

/**
 * @author god-jiang
 * @date 2020/1/24  18:39
 */
public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int res = target - nums[i];
            if (map.size() > 0 && map.containsKey(res)) {
                return new int[]{map.get(res), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{};
    }
}
```

## leetcode通过截图

![img](/images/N数之和/2.jpg)

## 复杂度分析

> 因为遍历一次就得到结果，所以时间复杂度为O(N)。然后就是因为利用哈希表开辟了跟数组一样长度的空间N，所以空间复杂度为O(N)。

------

## 题目2描述（三数之和）

![img](/images/N数之和/3.jpg)

## 解题思路

> 先固定第一个数，然后就变成了两数之和，解法和上面一样。然后这道题可以用双指针解，先将数组排序完，然后遍历的时候先固定一个数，剩下就是左指针和右指针相互移动来解出这道题。细节直接上代码好了

## 代码

```java
package leetcode;

import java.util.*;

/**
 * @author god-jiang
 * @date 2020/1/24  19:32
 */
public class ThreeSum {
    public static List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums == null || nums.length < 3) {
            return result;
        }
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            if (nums[i] > 0) {
                break;
            }
            //去重操作
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    //去重操作
                    while (left < right && nums[left] == nums[left + 1]) {
                        left++;
                    }
                    //去重操作
                    while (left < right && nums[right] == nums[right - 1]) {
                        right--;
                    }
                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return result;
    }
}
```

## leetcode通过截图

![img](/images/N数之和/4.jpg)

## 复杂度分析

> 因为一开始数组的排序过程的时间复杂度为O(N*logN)，然后就是固定一个值，通过移动左右指针来获得结果，时间复杂度为O(N^2)，空间复杂度因为没有引入额外的空间变量，所以空间复杂度为O(1)

## 总结

> 通过**两数之和** 和 **三数之和**两道题，对于四数之和或者五数之和又有什么不一样呢，大不了固定一个值变成三数之和，只要掌握了核心，再怎么变化我觉得都是可以解出来的，只不过会复杂一点，百变不离其中就是这么一个道理。



**PS：今晚刚吃完年夜饭就来更新leetcode的题解了，选择的是比较简单的两道相似题目（两数之和&三数之和），讲解了一下大概解法还有复杂度的分析，觉得还是挺入门级别的题目，利用这两道题可以明白到哈希表的好用，利用“空间换时间”，就这样吧。觉得博主写的还可以的可以点点赞，关注一波，谢谢大家的支持了~~~**