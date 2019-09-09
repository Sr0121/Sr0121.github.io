---
title: 'LeetCode:223. Rectangle Area'
date: 2019-08-31 14:45:19
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Find the total area covered by two **rectilinear** rectangles in a **2D** plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

![Rectangle Area](https://assets.leetcode.com/uploads/2018/10/22/rectangle_area.png)

**Example:**

```
Input: A = -3, B = 0, C = 3, D = 4, E = 0, F = -1, G = 9, H = 2
Output: 45
```

**Note:**

Assume that the total area is never beyond the maximum possible value of **int**.

<!--more-->



这题的核心就是求重叠部分的面积。

实际上，重叠部分的左下角为(max(A, E), max(B, F))，右上角为(min(C, G), min(D, H))，如果左下角的点不在右上角的点的左下方，则重叠面积为0。

**代码实现**

```python
class Solution:
    def computeArea(self, A: int, B: int, C: int, D: int, E: int, F: int, G: int, H: int) -> int:
        result = (C-A) * (D-B) + (G-E) * (H-F)
        rtx = min(C, G)
        rty = min(D, H)
        ldx = max(A, E)
        ldy = max(B, F)

        if ldx > rtx or ldy > rty:
            return result
        else:
            result -= (rtx - ldx) * (rty - ldy)
            return result

```

