---
title: 'LeetCode:216. Combination Sum III'
date: 2019-07-01 21:59:46
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Find all possible combinations of **k** numbers that add up to a number **n**, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

**Note:**

- All numbers will be positive integers.
- The solution set must not contain duplicate combinations.

**Example 1:**

```
Input: k = 3, n = 7
Output: [[1,2,4]]
```

**Example 2:**

```
Input: k = 3, n = 9
Output: [[1,2,6], [1,3,5], [2,3,4]]
```

<!--more-->

使用DFS查找可以很快找到所有的组合。

**代码实现**

```python
import copy

class Solution:
    def combinationSum3(self, k: int, n: int) -> 'list[list[int]]':
        def dfs(current, sum):
            if len(current) == k and sum == n:
                result.append(copy.deepcopy(current))
                return

            if sum >= n or len(current) >= k:
                return

            start = 1 if len(current) == 0 else current[-1] + 1
            for i in range(start, 10, 1):
                sum += i
                current.append(i)
                dfs(current, sum)
                sum -= i
                current.pop()

        result = []
        dfs([], 0)
        return result
```

