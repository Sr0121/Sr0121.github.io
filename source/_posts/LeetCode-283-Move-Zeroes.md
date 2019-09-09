---
title: 'LeetCode: 283. Move Zeroes'
date: 2019-09-06 22:08:18
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.

<!--more-->



题目要求inplace without making a copy对两个索引从左到右进行遍历，第一个索引index1遍历到0元素就停下，然后第二个索引index2继续遍历，直到第一个非零元素且index2>index1就停下，然后交换元素的值即可。

**代码实现**

```python
class Solution:
    def moveZeroes(self, nums: 'list[int]') -> 'None':
        """
        Do not return anything, modify nums in-place instead.
        """
        indexZero = 0
        indexNonZero = 0
        while True:
            while indexZero < len(nums):
                if nums[indexZero] == 0:
                    break
                indexZero += 1
            if indexZero == len(nums):
                break

            while indexNonZero < len(nums):
                if nums[indexNonZero] != 0 and indexNonZero > indexZero:
                    break
                indexNonZero += 1
            if indexNonZero == len(nums):
                break
            nums[indexZero] = nums[indexNonZero]
            nums[indexNonZero] = 0
```

