---
title: 'LeetCode:152. Maximum Product Subarray'
date: 2019-06-11 17:06:58
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example 1:**

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```


<!--more-->

本题和之前求连续子序列的最大和的那题很像。但是乘法与加法不同，还需要考虑两个负数的乘积很大的情况。

在这里，我用的解法是动态规划。对于序列nums，为了求解出最大的连续子序列的最大乘积，需要维护三个数组，分别为max_local, min_local和max_global。max_local[i]的含义是，以索引为i结束的连续子序列的乘积最大值；min_local[i]的含义是，以索引为i结束的连续子序列的乘积最小值，max_global[i]为到索引i为止，全局的乘积最大值。其中max_local[0], min_local[0]以及max_global[0]都为nums[0]。动态规划的状态转移公式为：

```python
max_local[i] = max(max_local[i-1]*nums[i], min_local[i-1]*nums[i], nums[i])
min_local[i] = min(max_local[i-1]*nums[i], min_local[i-1]*nums[i], nums[i])
max_global[i] = max(max_local[i], max_global[i-1])
```



**代码实现**

```python
class Solution:
    def maxProduct(self, nums: 'list[int]') -> 'int':
        if len(nums) == 0:
            return 0

        max_local = [0] * len(nums)
        min_local = [0] * len(nums)
        max_global = [0] * len(nums)

        max_local[0] = nums[0]
        min_local[0] = nums[0]
        max_global[0] = nums[0]

        for i in range(1, len(nums)):
            max_local[i] = max(max_local[i-1] * nums[i], min_local[i-1] * nums[i], nums[i])
            min_local[i] = min(max_local[i-1] * nums[i], min_local[i-1] * nums[i], nums[i])
            max_global[i] = max(max_global[i-1], max_local[i])

        return max_global[-1]


```

