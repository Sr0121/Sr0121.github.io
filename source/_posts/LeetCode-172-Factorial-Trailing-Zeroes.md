---
title: 'LeetCode:172. Factorial Trailing Zeroes'
date: 2019-06-16 23:04:16
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given an integer *n*, return the number of trailing zeroes in *n*!.

**Example 1:**

```
Input: 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```

**Example 2:**

```
Input: 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```

**Note:** Your solution should be in logarithmic time complexity.

<!--more-->

在阶乘中，只有5的倍数能产生0，因此这道题就转化成了n!的因子中有多少个5.

这里需要注意的是，25，125这种数字包含了多个5，需要进行重复计算。

**代码实现**

```python
class Solution:
    def trailingZeroes(self, n: int) -> int:
        divisor = 5
        result = 0
        while divisor <= n:
            result += n // divisor
            divisor *= 5
        return result
```

