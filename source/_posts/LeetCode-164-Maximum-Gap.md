---
title: 'LeetCode:164. Maximum Gap'
date: 2019-06-14 22:32:08
categories: LeetCode
tags: 
  - LeetCode
  - C++
---

**题目概述**

Given an unsorted array, find the maximum difference between the successive elements in its sorted form.

Return 0 if the array contains less than 2 elements.

**Example 1:**

```
Input: [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1,3,6,9], either
             (3,6) or (6,9) has the maximum difference 3.
```

**Example 2:**

```
Input: [10]
Output: 0
Explanation: The array contains less than 2 elements, therefore return 0.
```

**Note:**

- You may assume all elements in the array are non-negative integers and fit in the 32-bit signed integer range.
- Try to solve it in linear time/space.


<!--more-->

本题最难的地方就是要求时间和空间复杂度都为O(n)

所以本题的思路就是使用桶排序，因为这是一种时间复杂度和空间复杂度都为O(n)的排序算法。但是本题要求的不仅是排序，还需要算出数与数之间最大的Gap。

参考了网上的一些做法后，我也逐渐理清了思路。

首先，这个最大gap的值，不可能小于(maxNum-minNum)/size的值，其中maxNum和minNum为数组中的最大值和最小值，而size则为输入的数组大小。

考虑到这点，我们就可以用size+1个桶来存放nums中的所有数字。每个桶的大小为(maxNum-minNum)/size，存放的桶的索引值则为(i-minNum)/size。这样，我们就只需要找到每个桶的最大值和最小值，并且来比较桶与桶之间的最大Gap，这个最大Gap就是整个数组的最大Gap。（因为桶内的两个数的最大Gap不可能成为全局最大Gap）

由于不需要进行数与数之间的比较，本算法的时间复杂度和空间复杂度都是线性的。

**代码实现**

```c++
class Solution {
public:
    int maximumGap(vector<int>& nums) {
        if (nums.size() < 2) {
            return 0;
        }

        int maxNum = INT_MIN;
        int minNum = INT_MAX;
        for (auto i:nums) {
            if (i < minNum) {
                minNum = i;
            }
            if (i > maxNum) {
                maxNum = i;
            }
        }

        if (maxNum == minNum)
            return 0;
        int len = nums.size();
        int bucketSize = ceil((double)(maxNum-minNum)/nums.size());
        int bucketNum = nums.size()+1;
        vector<vector<int>> bucket(bucketNum);
        for (auto i:bucket) {
            i.resize(0);
        }

        for (auto i:nums) {
            int index = (i-minNum)/bucketSize;
            bucket[index].push_back(i);
        }

        int result = INT_MIN;

        vector<bool> isValid(bucketNum);
        vector<int> bucketMin(bucketNum);
        vector<int> bucketMax(bucketNum);
        for (int i = 0; i < bucketNum; i++) {
            if (bucket[i].size() > 0){
                isValid[i] = true;
                int tmpMin = INT_MAX;
                int tmpMax = INT_MIN;
                for (int j = 0; j < bucket[i].size(); j++){
                    if (bucket[i][j] < tmpMin)
                        tmpMin = bucket[i][j];
                    if (bucket[i][j] > tmpMax)
                        tmpMax = bucket[i][j];
                }
                bucketMin[i] = tmpMin;
                bucketMax[i] = tmpMax;
            } else {
                isValid[i] = false;
            }
        }

        int lastMax = bucketMax[0];
        for (int i = 1; i < bucketNum; i++) {
            if (!isValid[i])
                continue;
            result = result > bucketMin[i] - lastMax ? result : bucketMin[i] - lastMax;
            lastMax = bucketMax[i];
        }
        return result;
    }
};
```

