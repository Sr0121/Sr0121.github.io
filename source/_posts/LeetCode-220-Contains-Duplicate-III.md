---
title: 'LeetCode:220. Contains Duplicate III'
date: 2019-08-29 20:14:46
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an array of integers, find out whether there are two distinct indices *i* and *j* in the array such that the **absolute**difference between **nums[i]** and **nums[j]** is at most *t* and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3, t = 0
Output: true
```

**Example 2:**

```
Input: nums = [1,0,1,1], k = 1, t = 2
Output: true
```

**Example 3:**

```
Input: nums = [1,5,9,1,5,9], k = 2, t = 3
Output: false
```

<!--more-->



这题时间复杂度为O(n)的方法比较巧妙，将nums里的所有数字除以t后向下取整得到modifiedNums，如果modifiedNums中有两个数字相同，那么它们一定会相差t以内，因此一定返回True，如果没有两个数字相同，那么就去查找比它小1或大1的数字，然后比较它们对应的原数字是否相差t以内。

但是这题要使用一个滑动窗口和一个字典来进行操作。滑动窗口来满足索引差值在k以内，字典的键为modifiedNums中的数字，值为nums中的数字，主要是为了查找到某个键是否在modifiedNums中（如果有直接返回True），以及方便查找原数字的值。字典操作的复杂度都为O(n)。

坑的点主要是t为0的时候，这个时候的情况和t为1的情况其实是一样的。

**代码实现**

```python
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: 'list[int]', k: 'int', t: 'int') -> 'bool':
        if len(nums) <= 1:
            return False
        if k < 0 or t < 0:
            return False

        modifiedNums = [i//max(1, t) for i in nums]
        leftIndex = 0
        bucket = {modifiedNums[0]: nums[0]}
        for rightIndex in range(1, len(nums)):
            if rightIndex - leftIndex > k:
                del bucket[modifiedNums[leftIndex]]
                leftIndex += 1
            if modifiedNums[rightIndex] in bucket.keys():
                return True
            if modifiedNums[rightIndex] - 1 in bucket.keys() and abs(
                bucket[modifiedNums[rightIndex] - 1] - nums[rightIndex]) <= t:
                return True
            if modifiedNums[rightIndex] + 1 in bucket.keys() and abs(
                bucket[modifiedNums[rightIndex] + 1] - nums[rightIndex]) <= t:
                return True
            bucket[modifiedNums[rightIndex]] = nums[rightIndex]

        return False
```

