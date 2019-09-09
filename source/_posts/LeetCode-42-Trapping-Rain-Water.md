---
title: 'LeetCode: 42. Trapping Rain Water'
date: 2019-09-01 23:08:33
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

<!--more-->



这道题目要计算储水量是多少。对于每一个索引i，它的水量的高度为从左边到i点的最高的墙的高度max( : i)，和从i点到最右边的最高墙的高度max( i: )的最小值，即min( max( : i), max( i: ) )

对于每个点，找左边墙的最高高度有O(n)算法，即从左向右遍历，并且保存遍历的最大值，该最大值就是每个点的左墙高度，同理找右边墙的最高高度也有O(n)算法。

举个例子，对于[0,1,0,2,1,0,1,3,2,1,2,1]来说，对于每个索引的左墙最高度为[0, 1, 1, 2, 2, 2, 2, 3, 3, 3, 3, 3]，右墙高度为[3, 3, 3, 3, 3, 3, 3, 3, 2, 2, 2, 1]。

在找到两遍的墙的最大值之后，对于每个点，该点的左右墙的最小值即为水的高度。上述例子的最终水面高度就是[0, 1, 1, 2, 2, 2, 2, 3, 2, 2, 2, 1]，最后，减去原本的墙的高度，就可以得到结果。

```python
class Solution:
    def trap(self, height: 'list[int]') -> 'int':
        maxHeight = [0] * len(height)
        tmpMax = 0
        for i in range(len(maxHeight)):
            tmpMax = height[i] if height[i] > tmpMax else tmpMax
            maxHeight[i] = tmpMax

        tmpMax = 0
        for i in range(len(maxHeight)-1, -1, -1):
            tmpMax = height[i] if height[i] > tmpMax else tmpMax
            maxHeight[i] = tmpMax if tmpMax < maxHeight[i] else maxHeight[i]

        result = 0
        for i in range(len(maxHeight)):
            result += (maxHeight[i] - height[i])

        return result
```

