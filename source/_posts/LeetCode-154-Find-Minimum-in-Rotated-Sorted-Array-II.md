---
title: 'LeetCode:154. Find Minimum in Rotated Sorted Array II'
date: 2019-06-12 15:28:56
categories: LeetCode
tags: 
  - LeetCode
  - C++
---

**题目概述**

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element.

The array may contain duplicates.

**Example 1:**

```
Input: [1,3,5]
Output: 1
```

**Example 2:**

```
Input: [2,2,2,0,1]
Output: 0
```


<!--more-->

同理LeetCode: 153. Find Minimum in Rotated Sorted Array



**代码实现**

```python
class Solution:
    def findMin(self, nums: 'list[int]') -> 'int':
        for i in range(1, len(nums)):
            if nums[i] < nums[i-1]:
                return nums[i]
        return nums[0]
```

