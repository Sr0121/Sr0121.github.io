---
title: 'LeetCode: 377. Combination Sum IV'
date: 2019-09-09 00:07:51
categories: LeetCode
tags:
  - LeetCode
  - C++
---

**题目描述**

Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

**Example:**

```
nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```

<!--more-->



一开始以为是一道简单的dfs的题目，结果暴力做直接TLE。

这题应该用DP来做，令`dp[i]`为这个序列和为i的排列个数。状态转移方程为:

$$dp_{i} = \sum_jdp_{i-j}\\j\in nums$$

意思就是$j$是nums中的数字，这个dp的规律就是对于目标和target，它是所有和为target-j的可能性之和，相当于在所有target-j的目标最后加上了j作为一个新的排列。

**代码实现**

```c++
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<unsigned long> dp(target+1, 0);
        dp[0] = 1;
        for (int i=1; i<=target; i++) {
            for (auto it = nums.begin(); it != nums.end(); it++) {
                if (i - *it >= 0) {
                    dp[i] += dp[i - *it];
                }
            }
        }

        return dp[target];
    }
};
```

