---
title: 'LeetCode:200. Number of Islands'
date: 2019-06-19 23:35:53
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```
Input:
11000
11000
00100
00011

Output: 3
```

<!--more-->

这题需要一个额外的二维数组，来记录某一个点是否被检查过。然后我们需要对所有的点按顺序进行一次深度优先搜索，如果说这个点已经被检查过，则不再搜索。那么，一开始需要进行搜索的点的个数，就是岛屿的数量。

**代码实现**

```python
class Solution:
    def __init__(self):
        self.count = 0
        self.matrix = None

    def numIslands(self, grid: 'list[list[str]]') -> 'int':
        if len(grid) == 0:
            return 0
        if len(grid[0]) == 0:
            return 0

        self.matrix = [[0] * len(grid[0]) for _ in range(len(grid))]

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == '1' and self.matrix[i][j] == 0:
                    self.count += 1
                    self.dfs(i, j, grid)

        return self.count

    def dfs(self, x, y, grid):
        if grid[x][y] == '1':
            self.matrix[x][y] = 1
            if x > 0 and self.matrix[x-1][y] == 0:
                self.dfs(x-1, y, grid)
            if y > 0 and self.matrix[x][y-1] == 0:
                self.dfs(x, y-1, grid)
            if x < len(grid)-1 and self.matrix[x+1][y] == 0:
                self.dfs(x+1, y, grid)
            if y < len(grid[0])-1 and self.matrix[x][y+1] == 0:
                self.dfs(x, y+1, grid)

```

