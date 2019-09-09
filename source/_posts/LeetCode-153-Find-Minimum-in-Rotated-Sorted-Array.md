---
title: 'LeetCode:153. Find Minimum in Rotated Sorted Array'
date: 2019-06-12 15:24:24
categories: LeetCode
tags: 
  - LeetCode
  - Python
---

**题目概述**

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element.

You may assume no duplicate exists in the array.

**Example 1:**

```
Input: [3,4,5,1,2] 
Output: 1
```

**Example 2:**

```
Input: [4,5,6,7,0,1,2]
Output: 0
```


<!--more-->

由于输入的数组是通过有序的数组进行旋转后得到的，因此在从左向右遍历的时候，突然变小的那个数字一定是全局最小值



**代码实现**

```python
class Solution:
    def findMin(self, nums: 'list[int]') -> 'int':
        for i in range(1, len(nums)):
            if nums[i] < nums[i-1]:
                return nums[i]
        return nums[0]
```

