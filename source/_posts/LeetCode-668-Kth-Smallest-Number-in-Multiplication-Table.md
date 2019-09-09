---
title: 'LeetCode: 668. Kth Smallest Number in Multiplication Table'
date: 2019-09-08 23:13:57
categories: LeetCode
tags:
  - Python
  - LeetCode
---

**题目描述**

Nearly every one have used the [Multiplication Table](https://en.wikipedia.org/wiki/Multiplication_table). But could you find out the `k-th` smallest number quickly from the multiplication table?

Given the height `m` and the length `n` of a `m * n` Multiplication Table, and a positive integer `k`, you need to return the `k-th` smallest number in this table.

**Example 1:**

```
Input: m = 3, n = 3, k = 5
Output: 
Explanation: 
The Multiplication Table:
1	2	3
2	4	6
3	6	9

The 5-th smallest number is 3 (1, 2, 2, 3, 3).
```



**Example 2:**

```
Input: m = 2, n = 3, k = 6
Output: 
Explanation: 
The Multiplication Table:
1	2	3
2	4	6

The 6-th smallest number is 6 (1, 2, 2, 3, 4, 6).
```

<!--more-->



真的是挺难的一道二分查找题，主要也是想不到可以这么做。

令`left = 1`,`right=m*n`得到`mid`然后去计算multiplication table中小于`mid`的个数`cnt`。如果小于，则令`right=mid`否则则`left=mid+1`，最后返回`left`。

这里可以不用考虑left是否在table中，因为这样做的话是肯定在table里的。因为`left`一定能找到一个在table中的数字，满足在table中的条件，如果找到了，那么left就不会有变化了，接下来都是`right`在进行收敛。另外，这里不能用`right=mid-1`，是因为`mid`得到的`cnt`是一个大于等于实际`k`的值(比如第一个例子，mid为6的时候，cnt为8，如果在k=7点时候直接right=mid-1的话，会永远找不到值)，所以`right=mid`，而在`left=mid+1`则没有问题。

**代码实现**

```python
class Solution {
public:
    int findKthNumber(int m, int n, int k) {
        int left = 1;
        int right = n*m;
        while (left < right) {
            int mid = (right - left) / 2 + left;
            int cnt = 0;
            for (int i = 1; i <= m; i++) {
                cnt += min(mid/i, n);
            }
            if (cnt < k) {
                left = mid+1;
            } else {
                right = mid;
            }
        }
        return left;
    }
};
```

