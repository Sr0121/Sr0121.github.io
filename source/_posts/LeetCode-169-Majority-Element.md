---
title: 'LeetCode:169. Majority Element'
date: 2019-06-16 21:41:12
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```
Input: [3,2,3]
Output: 3
```

**Example 2:**

```
Input: [2,2,1,1,1,2,2]
Output: 2
```

<!--more-->

题目要求找到数组中的众数。我是把数组进行排序后从左到右找，如果当前数字和之前的数字一样，就会给一个记录值加一，如果发现当前数字与其之前的数字不一样，则把记录值和全局最大值进行比较。

**代码实现**

```python
class Solution:
    def majorityElement(self, nums: 'list[int]') -> 'int':
        nums = sorted(nums)
        if len(nums) == 1:
            return nums[0]

        maxNum = 1
        tmpNum = 1
        targetIndex = 0
        for i in range(1, len(nums)):
            if nums[i] == nums[i-1]:
                tmpNum += 1
            elif i < len(nums):
                if tmpNum >= maxNum:
                    targetIndex = i-1
                    maxNum = tmpNum
                tmpNum = 1
            if i == len(nums)-1 and tmpNum >= maxNum:
                targetIndex = i

        return nums[targetIndex]
```

