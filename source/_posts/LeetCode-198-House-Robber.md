---
title: 'LeetCode:198. House Robber'
date: 2019-06-19 16:33:02
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```


<!--more-->

这题就是一个很明显的动态规划。由于两次偷盗的索引不能相邻，因此某个索引的偷盗最大值为上个索引的偷盗最大值或上上个索引的偷盗值加上当前nums的值，即`dp[i] = max(dp[i-1], dp[i-2] + nums[i])`

**代码实现**

```python
class Solution:
    def rob(self, nums: 'list[int]') -> 'int':
        if len(nums) == 0:
            return 0
        dp = [0] * len(nums)
        dp[0] = nums[0]
        if len(nums) == 1:
            return dp[0]

        dp[1] = max(nums[0], nums[1])
        for i in range(2, len(dp)):
            dp[i] = max(dp[i-1], dp[i-2] + nums[i])

        return dp[-1]

```

