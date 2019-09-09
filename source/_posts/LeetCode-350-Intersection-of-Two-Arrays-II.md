---
title: 'LeetCode: 350. Intersection of Two Arrays II'
date: 2019-09-07 15:31:30
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given two arrays, write a function to compute their intersection.

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

<!--more-->



这里我使用了一个dict来存放nums1中的数字，其中key为nums1的数字，value为该key出现在nums1中的次数。然后遍历nums2，并且在dict中查找是否出现过这个key，如果有，则给该key的value-=1，并且在result中加入一次这个key，如果value变成了0，就pop这个key。

**代码实现**

```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        dic1 = {}
        for num in nums1:
            if num in dic1.keys():
                dic1[num] += 1
            else:
                dic1[num] = 1

        result = []
        for num in nums2:
            if num in dic1.keys():
                dic1[num] -= 1
                result.append(num)
                if dic1[num] == 0:
                    dic1.pop(num)
        return result
```

