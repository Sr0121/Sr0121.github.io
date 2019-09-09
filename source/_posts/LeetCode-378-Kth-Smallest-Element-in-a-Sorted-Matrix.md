---
title: 'LeetCode: 378. Kth Smallest Element in a Sorted Matrix'
date: 2019-09-08 14:47:42
categories: LeetCode
tags:
  - LeetCode
  - C++
---

**题目描述**

Given a *n* x *n* matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```

<!--more-->



这题我想不到什么更好的方法，并没有用到行列之间的有序性来做，只是维持了一个最大堆（优先序列）去做，不过OJ还是可以通过的。 

**代码实现**

```c++
class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        priority_queue<int> priorityQueue;
        for(int i = 0; i < matrix.size(); i++) {
            for(int j=0; j < matrix[0].size(); j++) {
                priorityQueue.push(matrix[i][j]);
                if (priorityQueue.size() > k) {
                    priorityQueue.pop();
                }
            }
        }
        return priorityQueue.top();
    }
};
```

