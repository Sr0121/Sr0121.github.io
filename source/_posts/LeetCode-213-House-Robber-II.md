---
title: 'LeetCode:213. House Robber II'
date: 2019-06-27 17:20:12
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
```

**Example 2:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```


<!--more-->

本题是之前House Robber的升级版。在这里，所有的房子形成一个环形，言下之意就是第一个房子和最后一个房子不能都偷。

假设有n个房子，他们的财产为house[0], house[1], ..., house[n-1]，要保证house[0]和house[n-1]都不被偷，并且求出能偷的最大值。如果不偷house[n-1]，那么就转化成了House Robber中的house[0], ..., house[n-2]的情形；同理，如果不偷house[0]，那么就转化成了求house[1], ..., house[n-1]的情形。因此，本题就是求House Robber中的house[0], ..., house[n-2]和house[1], ..., house[n-1]的最大值。

**代码实现**

```python
class Solution:
    def rob1(self, nums) -> 'list[int]':
        if len(nums) <= 2:
            return max(nums)

        dp = [0] * len(nums)

        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])

        for i in range(2, len(nums)):
            dp[i] = max(dp[i-1], dp[i-2] + nums[i])

        return dp

    def rob2(self, nums) -> 'list[int]':
        if len(nums) <= 2:
            return max(nums)

        dp = [0] * len(nums)

        dp[len(nums)-1] = nums[len(nums)-1]
        dp[len(nums)-2] = max(nums[len(nums)-1], nums[len(nums)-2])

        for i in range(len(nums)-3, -1, -1):
            dp[i] = max(dp[i+1], dp[i+2] + nums[i])

        return dp

    def rob(self, nums: 'list[int]') -> 'int':
        if len(nums) <= 2:
            return max(nums)

        dp1 = self.rob1(nums)
        dp2 = self.rob2(nums)

        return max(dp1[-2], dp2[1])

```

