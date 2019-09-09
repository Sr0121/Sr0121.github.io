---
title: 'LeetCode: 228. Summary Ranges'
date: 2019-09-02 17:12:41
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a sorted integer array without duplicates, return the summary of its ranges.

**Example 1:**

```
Input:  [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: 0,1,2 form a continuous range; 4,5 form a continuous range.
```

**Example 2:**

```
Input:  [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: 2,3,4 form a continuous range; 8,9 form a continuous range.
```

<!--more-->



题目要我们返回所有数字的范围，这些数字已经有序排好，并且没有重复。

这里需要从左向右遍历，当遍历到i，且nums[i] != nums[i-1]+1的时候，i-1就是一个range的右边界，i是下一个边界的左边界。另外需要注意左边界和右边界相同的情况。

为了方便代码的实现，我在输入数组后加入了一个dummy元素，这个元素理论上可以是任何值，它可以让代码更简单，而不需要考虑最后一个值的边界情况。

```python
class Solution:
    def summaryRanges(self, nums: 'list[int]') -> 'list[str]':
        result = []
        if len(nums) == 0:
            return result

        start = nums[0]
        if len(nums) == 1:
            result.append(str(start))
            return result

        nums.append(nums[0])

        for i in range(1, len(nums)):
            if nums[i - 1] == nums[i] - 1:
                continue
            else:
                if start != nums[i - 1]:
                    result.append(str(start) + '->' + str(nums[i - 1]))
                else:
                    result.append(str(start))
                start = nums[i]

        return result

```

