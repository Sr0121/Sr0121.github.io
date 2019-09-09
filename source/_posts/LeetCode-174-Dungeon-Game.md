---
title: 'LeetCode:174. Dungeon Game'
date: 2019-06-19 15:41:44
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

The demons had captured the princess (**P**) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (**K**) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health (*negative* integers) upon entering these rooms; other rooms are either empty (*0's*) or contain magic orbs that increase the knight's health (*positive* integers).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

 

**Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.**

For example, given the dungeon below, the initial health of the knight must be at least **7** if he follows the optimal path `RIGHT-> RIGHT -> DOWN -> DOWN`.

| -2 (K) | -3   | 3      |
| ------ | ---- | ------ |
| -5     | -10  | 1      |
| 10     | 30   | -5 (P) |

 

**Note:**

- The knight's health has no upper bound.
- Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.


<!--more-->

这道题目翻译一下，就是要保证这个骑士在走过每一个格子之后，血量至少为1。这题可以用动态规划来进行求解。如果一个格子上的数字为-5，那么骑士在踏上这个格子的时候，至少需要max(1, 1-(-5)) = 6点血量；如果格子上的数字为5，那么骑士只需要max(1, 1-5) = 1点血量。

接着需要考虑周围格子的情况。如果某个格子的右边的格子至少需要有4点血量，另一个格子至少要3点血量，那么在经过这个格子之后，我们需要至少保留min(4, 3) = 3点血量。

那么，状态转移公式就是`dp[i][j] = max(min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j], 1) `

**代码实现**

````python
class Solution:
    def calculateMinimumHP(self, dungeon: 'list[list[int]]') -> 'int':
        row = len(dungeon)
        column = len(dungeon[0])
        dp = [[0] * column for _ in range(row)]

        dp[row-1][column-1] = max(1 - dungeon[row-1][column-1], 1)

        for i in range(column-2, -1, -1):
            dp[row-1][i] = max(dp[row-1][i+1] - dungeon[row-1][i], 1)

        for i in range(row - 2, -1, -1):
            dp[i][column - 1] = max(dp[i + 1][column - 1] - dungeon[i][column - 1], 1)

        for i in range(row - 2, -1, -1):
            for j in range(column - 2, -1, -1):
                dp[i][j] = max(min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j], 1)

        return dp[0][0]
````

