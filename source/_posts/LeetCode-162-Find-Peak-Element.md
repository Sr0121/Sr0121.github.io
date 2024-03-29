---
title: 'LeetCode:162. Find Peak Element'
date: 2019-06-13 17:18:54categories: LeetCode
tags:
  - LeetCode
  - C++
---

**题目概述**

A peak element is an element that is greater than its neighbors.

Given an input array `nums`, where `nums[i] ≠ nums[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `nums[-1] = nums[n] = -∞`.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```
Input: nums = [1,2,1,3,5,6,4]
Output: 1 or 5 
Explanation: Your function can return either index number 1 where the peak element is 2, 
             or index number 5 where the peak element is 6.
```

**Note:**

Your solution should be in logarithmic complexity.


<!--more-->

就是对数组中的所有元素从做向右遍历，然后找到比两边都大的元素的索引返回即可

**代码实现**

```c++
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        if (nums.size() == 1){
            return 0;
        }
        for (int i = 0; i < nums.size(); i++){
            if (i == 0) {
                if (nums[i] > nums[i+1])
                    return i;
            } else if (i == nums.size()-1) {
                if (nums[i] > nums[i-1])
                    return i;
            } else {
                if (nums[i] > nums[i+1] && nums[i] > nums[i-1])
                    return i;
            }
        }
        return 0;
    }
};
```

