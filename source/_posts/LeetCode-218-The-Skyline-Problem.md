---
title: 'LeetCode:218. The Skyline Problem'
date: 2019-07-02 23:52:06
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Now suppose you are **given the locations and height of all the buildings** as shown on a cityscape photo (Figure A), write a program to **output the skyline** formed by these buildings collectively (Figure B).



[![Buildings](https://assets.leetcode.com/uploads/2018/10/22/skyline1.png) ](https://leetcode.com/static/images/problemset/skyline1.jpg)[![Skyline Contour](https://assets.leetcode.com/uploads/2018/10/22/skyline2.png)](https://leetcode.com/static/images/problemset/skyline2.jpg)

The geometric information of each building is represented by a triplet of integers `[Li, Ri, Hi]`, where `Li` and `Ri`are the x coordinates of the left and right edge of the ith building, respectively, and `Hi` is its height. It is guaranteed that `0 ≤ Li, Ri ≤ INT_MAX`, `0 < Hi ≤ INT_MAX`, and `Ri - Li > 0`. You may assume all buildings are perfect rectangles grounded on an absolutely flat surface at height 0.

For instance, the dimensions of all buildings in Figure A are recorded as: `[ [2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8] ] `.

The output is a list of "**key points**" (red dots in Figure B) in the format of `[ [x1,y1], [x2, y2], [x3, y3], ... ]`that uniquely defines a skyline. **A key point is the left endpoint of a horizontal line segment**. Note that the last key point, where the rightmost building ends, is merely used to mark the termination of the skyline, and always has zero height. Also, the ground in between any two adjacent buildings should be considered part of the skyline contour.

For instance, the skyline in Figure B should be represented as:`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`.

**Notes:**

- The number of buildings in any input list is guaranteed to be in the range `[0, 10000]`.
- The input list is already sorted in ascending order by the left x position `Li`.
- The output list must be sorted by the x position.
- There must be no consecutive horizontal lines of equal height in the output skyline. For instance, `[...[2 3], [4 5], [7 5], [11 5], [12 7]...]` is not acceptable; the three lines of height 5 should be merged into one in the final output as such: `[...[2 3], [4 5], [12 7], ...]`

<!--more-->

题目需要让我们求出几个长方形组成的轮廓，返回的点唯一确定这个轮廓。从B图中可以发现，所有返回的点实际上为轮廓高度的突变点。而所有可能的突变点，均为长方形竖着的边。为了做区分，我把左边的边称为开始边，右边的边称为结束边。

因此，我们需要从左向右遍历矩形的开始边盒结束边，并且记录当前的最高点的高度。所以我们需要维护一个有序的list，当遍历到的边为开始边时，把开始边的高度增加到这个有序列表中，如果是结束边，则把该边的高度从列表中删除。

在实际操作的时候，我们需要把[Li, Ri, Hi]分解为[Li, -Hi]和[Ri, Hi]，然后统一存放到同一个数组中，并且根据Li和Ri的值进行无差别的排列。这样可以方便之后从左向右进行遍历，并且在遍历的同时能区分开始边和结束边。



在网上的一些方法中，有人使用了MaxHeap，这个堆可以很快地返回最大值，并且可以很方便地进行删除和增加操作，时间复杂度为O(n)。但是Python中需要对其进行额外实现，然而直接使用快速排序维持一个有序列表的方法也能通过OJ，所以在这里我就只是用了快速排序。

**代码实现**

```python
import functools

class Solution:
    def getSkyline(self, buildings: 'list[list[int]]') -> 'list[list[int]]':
        def cmp(x, y):
            if x[0] != y[0]:
                return x[0] - y[0]
            else:
                return x[1] - y[1]

        nodes = []
        result = []
        if len(buildings) == 0:
            return result

        for i in buildings:
            nodes.append([i[0], -i[2]])
            nodes.append([i[1], i[2]])

        nodes = sorted(nodes, key=functools.cmp_to_key(cmp))

        peak = 0
        peaks = [0]

        for i in nodes:
            if i[1] < 0:
                peaks.append(-i[1])
                peaks = sorted(peaks)
            else:
                peaks.remove(i[1])
            current = peaks[-1]
            if current != peak:
                result.append([i[0], current])
                peak = current

        return result


```

