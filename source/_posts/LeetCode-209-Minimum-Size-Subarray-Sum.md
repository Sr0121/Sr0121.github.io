---
title: 'LeetCode:209. Minimum Size Subarray Sum'
date: 2019-06-25 14:54:19
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

**Example:** 

```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

**Follow up:**

If you have figured out the *O*(*n*) solution, try coding another solution of which the time complexity is *O*(*n* log *n*). 

<!--more-->

题目要求在一串数字中找到最短的连续数字，让他们的和大于给定的正数。

这里需要记录数组的开始和结尾的索引，并且需要记录连续的数字之和。每当数字比给定目标小的时候，右边的索引要往右移动，其他情况则左边索引向右移动一格，并且如果比最小的结果更小的时候需要记录这个长度。

**代码实现**

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: 'list[int]') -> int:
        if len(nums) == 0:
            return 0
        
        start = 0
        end = 1
        sum = nums[0]
        result = len(nums)
        find = False
        while True:
            if sum >= s:
                find = True
                result = end - start if end - start < result else result
                if start < len(nums)-1:
                    sum -= nums[start]
                    start += 1
                else:
                    break
            else:
                if end < len(nums):
                    sum += nums[end]
                    end += 1
                else:
                    break

        return 0 if find == False else result

```

