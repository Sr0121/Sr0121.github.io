---
title: 'LeetCode: 349. Intersection of Two Arrays'
date: 2019-09-07 15:26:34
categories: LeetCode
tags:
  - Python
  - LeetCode
---

**题目描述**

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

**Note:**

- Each element in the result must be unique.
- The result can be in any order.

<!--more-->



用python的set投机取巧了一下hhh

**代码实现**

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        s1 = set(nums1)
        s2 = set(nums2)
        return list(s1 & s2)
```

