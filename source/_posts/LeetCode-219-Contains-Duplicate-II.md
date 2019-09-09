---
title: 'LeetCode:219. Contains Duplicate II'
date: 2019-07-03 10:37:47
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an array of integers and an integer *k*, find out whether there are two distinct indices *i* and *j* in the array such that **nums[i] = nums[j]** and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```
Input: nums = [1,2,3,1], k = 3
Output: true
```

**Example 2:**

```
Input: nums = [1,0,1,1], k = 1
Output: true
```

**Example 3:**

```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

<!--more-->

这题需要找数组中存在nums[i] == nums[j]，并且i和j的差的绝对值小于等于k。

这里需要用一个字典进行存储，字典的键为nums[i]，值为i。从左到右遍历数组nums，如果nums[i]没有出现在字典的键中，则添加nums[i]到字典里。如果字典中已经有nums[i]，则将比较i与该键所对应的值的差值，如果小于k则返回True，否则更新该值。

**代码实现**

```python
class Solution:
    def containsNearbyDuplicate(self, nums: 'list[int]', k: 'int') -> 'bool':
        M = {}
        for i in range(len(nums)):
            if nums[i] not in M.keys():
                M[nums[i]] = i
            else:
                if i - M[nums[i]] <= k:
                    return True
                else:
                    M[nums[i]] = i
        return False

```

