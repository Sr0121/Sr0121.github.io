---
title: 'LeetCode:189. Rotate Array'
date: 2019-08-28 22:54:35
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an array, rotate the array to the right by *k* steps, where *k* is non-negative.

**Example 1:**

```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

**Example 2:**

```
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

<!--more-->



利用另一个数组对结果进行存储。

**代码实现**

```python
class Solution:
    def rotate(self, nums: 'list[int]', k: 'int') -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        tmp = n * [0]
        
        for i in range(len(nums)):
            tmp[(i+k)%n] = nums[i]
        
        for i in range(len(nums)):
            nums[i] = tmp[i]
```

