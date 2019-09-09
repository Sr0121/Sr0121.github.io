---
title: 'LeetCode:188. Best Time to Buy and Sell Stock IV'
date: 2019-08-27 23:58:09
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Say you have an array for which the *i-*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete at most **k** transactions.

**Note:**
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

**Example 1:**

```
Input: [2,4,1], k = 2
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
```

**Example 2:**

```
Input: [3,2,6,5,0,3], k = 2
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
             Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
```

<!--more-->



这题可以看成两部分，当k很大的时候，和Best Time to Buy and Sell Stock II一样，可以看成无限次买卖。只要找到数组中的所有递增的子序列，并且求每个子序列两端的差值之和。

当k很小的时候，使用Best Time to Buy and Sell Stock III的DP算法。构建两个数组localMax和globalMax，其中localMax\[i][j]表示在第i天交易了j次，并且最后一天将股票卖出的最大值，而globalMax\[i][j]则是第i天交易了j次的最大值。状态转移方程为：

localMax\[i][j] = max(localMax\[i-1][j]+price[i]-price[i-1], globalMax\[i-1][j-1]+max(0, price[i]-price[i-1]))

globalMax\[i][j] = max(globalMax\[i][j-1], local\[i][j])

对于全局最优globalMax来说，在最后一天的买卖情况可以分为卖和不卖，如果不卖，那么globalMax\[i][j] = globalMax\[i][j-1]，因此我们需要用另一个状态转移方程来表示最后一天卖的情况，也就是localMax。

对于localMax来说，如果最后一天可以有三种情况得到。第一种是在对于localMax\[i-1][j]来说的最后一次买卖到第i天执行，也就是localMax\[i-1][j]+price[i]-price[i-1]；第二种可能是在i-1天交易j-1次时，对于全局最优globalMax\[i-1][j-1]来说，在倒数第二天和倒数第一天执行一次交易；最后一种情况则是在i-1天交易j-1次时，对于全局最优globalMax\[i-1][j-1]来说在最后一天买了又卖（得到0元），其中最后两种可以合并，即globalMax\[i-1][j-1]+max(0, price[i]-price[i-1])。这些情况的最大值就是localMax的新的状态。

**代码实现**

```python
class Solution:
    def maxProfit(self, k: 'int', prices: 'list[int]') -> 'int':
        def smallK():
            if len(prices) == 0 or k == 0:
                return 0
            times = min(k, len(prices)) + 1
            localMax = [times * [0] for _ in range(len(prices))]
            globalMax = [times * [0] for _ in range(len(prices))]
            for i in range(1, len(prices)):
                for j in range(1, times):
                    localMax[i][j] = max(localMax[i - 1][j] + prices[i] - prices[i - 1],
                                         globalMax[i - 1][j - 1] + max(prices[i] - prices[i - 1], 0))
                    globalMax[i][j] = max(globalMax[i - 1][j], localMax[i][j])
            return globalMax[-1][-1]

        def largeK():
            result = 0
            tmp = 0
            for i in range(1, len(prices)):
                if prices[i] < prices[i-1]:
                    result += tmp
                    tmp = 0
                else:
                    tmp += prices[i] - prices[i-1]
            return result

        if k < len(prices):
            return smallK()
        else:
            return largeK()
```

