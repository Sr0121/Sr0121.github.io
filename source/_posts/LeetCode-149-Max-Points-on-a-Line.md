---
title: 'LeetCode:149. Max Points on a Line'
date: 2019-06-10 21:50:12
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given *n* points on a 2D plane, find the maximum number of points that lie on the same straight line.

**Example 1:**

```
Input: [[1,1],[2,2],[3,3]]
Output: 3
Explanation:
^
|
|        o
|     o
|  o  
+------------->
0  1  2  3  4
```

**Example 2:**

```
Input: [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
Explanation:
^
|
|  o
|     o        o
|        o
|  o        o
+------------------->
0  1  2  3  4  5  6
```

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.


<!--more-->

这题比较坑，而且这个hard难度考察的也并不是算法。这题目最直观的想法是通过求两点的直线方程后，对所有点进行遍历并记数。我们需要求到两点之间的斜率等信息。

但是，本题要考虑的还有：

1. 如何尽量避免重复的运算
2. 对平行于Y轴的直线的特殊处理
3. 需要考虑除法带来的一些计算问题：计算机内部的除法得到的值并非是一个分数，而是一个有限小数。比如对于[1,1]、[4,2]两点，通过求解得到的斜率不是正好的1/3，而是类似0.33333的有限小数，因此尽管点[7,3]在这条直线上，但是使用0.33333*(7-1)+1-3得到的并不是0，而是一个很接近0的数字，因此需要尽量避免使用除法



因此，在本题中，我使用了checkMetrix来表示两个点之间是否已经经过了计算，并且使用乘法代替除法



**代码实现**

```python
class Solution(object):
    def __init__(self):
        self.checkMetrix = None

    def maxPoints(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        wordLen = len(points)
        self.checkMetrix = [[0] * wordLen for _ in range(wordLen)]
        maxCount = 0
        flag = 0

        for i in range(wordLen):
            for j in range(wordLen):
                if self.checkMetrix[i][j] == 1:
                    continue
                if i == j:
                    continue
                if points[i][0] == points[j][0] and points[i][1] == points[j][1]:
                    continue
                maxCount = max(self.countPoints(i, j, points), maxCount)
                flag = 1
        if flag == 0:
            return wordLen
        else:
            return maxCount

    def countPoints(self, index1, index2, points):
        point1 = points[index1]
        point2 = points[index2]
        count = 0
        if point1[0] == point2[0]:
            for i in range(len(points)):
                if points[i][0] == point1[0]:
                    self.checkMetrix[i][index1] = 1
                    self.checkMetrix[i][index2] = 1
                    self.checkMetrix[index1][i] = 1
                    self.checkMetrix[index2][i] = 1
                    count += 1
        else:
            for i in range(len(points)):
                if (point1[1] - point2[1]) * (points[i][0]-point1[0]) == (points[i][1] - point1[1]) * (point1[0] - point2[0]):
                    self.checkMetrix[i][index1] = 1
                    self.checkMetrix[i][index2] = 1
                    self.checkMetrix[index1][i] = 1
                    self.checkMetrix[index2][i] = 1
                    count += 1
        return count


```



l

