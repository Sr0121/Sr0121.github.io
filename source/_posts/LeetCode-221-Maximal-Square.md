---
title: 'LeetCode:221. Maximal Square'
date: 2019-08-29 21:25:45
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**

```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

<!--more-->



这题最快的方法还是使用动态规划。当matrix\[i][j]为0时，dp\[i][j]为0，当matrix\[i][j]为1时，状态转移方程为：

dp\[i][j] = min(dp\[i-1][j-1], dp\[i][j-1], dp\[i-1][j]) + 1

dp\[i][j]表示从左上角到matrix\[i][j]的最大的正方形的边长。在每一个matrix为1的点，需要看它左上方，上方和左边的dp值，取最小的+1，才是当前的dp。因为最小的边长才是制约dp\[i][j]大小的因素。

**代码实现**

```python
class Solution:
    def maximalSquare(self, matrix: 'List[List[str]]') -> 'int':
        n = len(matrix)
        if n == 0:
            return 0
        m = len(matrix[0])
        if m == 0:
            return 0

        dp = [[0] * m for _ in range(n)]
        for i in range(n):
            if matrix[i][0] == "1":
                dp[i][0] = 1

        for j in range(m):
            if matrix[0][j] == "1":
                dp[0][j] = 1

        for i in range(1, n):
            for j in range(1, m):
                if matrix[i][j] == "1":
                    dp[i][j] = min(dp[i][j - 1], dp[i - 1][j], dp[i - 1][j - 1]) + 1

        result = 0

        for i in range(0, n):
            for j in range(0, m):
                result = max(dp[i][j], result)

        return result**2


```

