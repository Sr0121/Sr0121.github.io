---
title: 'LeetCode: 480. Sliding Window Median'
date: 2019-09-08 13:46:17
categories: LeetCode
tags:
  - LeetCode
  - C++
---

**题目描述**

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples: 

```
[2,3,4]` , the median is `3
[2,3]`, the median is `(2 + 3) / 2 = 2.5
```

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Your job is to output the median array for each window in the original array.

For example,
Given *nums* = `[1,3,-1,-3,5,3,6,7]`, and *k* = 3.

```
Window position                Median
---------------               -----
[1  3  -1] -3  5  3  6  7       1
 1 [3  -1  -3] 5  3  6  7       -1
 1  3 [-1  -3  5] 3  6  7       -1
 1  3  -1 [-3  5  3] 6  7       3
 1  3  -1  -3 [5  3  6] 7       5
 1  3  -1  -3  5 [3  6  7]      6
```

Therefore, return the median sliding window as `[1,-1,-1,3,5,6]`.

**Note:** 
You may assume `k` is always valid, ie: `k` is always smaller than input array's size for non-empty array.

<!--more-->



这题和之前的着sliding window中的最大值不一样，之前只需要维护好最大值就可以了，但是这里还是需要维护整个数组的顺序。在这个时候，效率最高的是multiset，本质是一个红黑树，插入、查找、删除的时间复杂度均为O(logn)。

在这里我们需要用一个iterator确定中间值的位置，可以使用`auto it = next(multiset, k/2)`实现。在确定了初始中间iterator的位置后，每次向右滑动时，都要将新元素加入multiset，同时比较这个值和\*iterator的大小，如果比较小，那么它一定排在iterator之前，为了让iterator仍然指向中间的位置，我们需要`iterator--`（这里不能取等，因为相同的元素在multiset中，新的排在旧的之后） 。同时，还需要将window最左边的元素erase出multiset，如果这个值不大于\*iterator，那么需要`iterator++`（这里需要去等号，因为等会删除的时候，对于任何不大于\*iterator的\*it，it一定在iterator前）

最后要在multiset中删除元素，multiset不能直接用erase，不然会删除所有相同的元素，而应该使用multiset.find(n)找到第一个it，然后用it删除。最后时间复杂度为O(nlogk)

**代码实现**

```c++
class Solution {
public:
    vector<double> medianSlidingWindow(vector<int>& nums, int k) {
        vector<double> result;
        multiset<double> window(nums.begin(), nums.begin()+k);
        auto midIterator = next(window.begin(), k/2);

        for (int i = k; i <= nums.size(); i++) {
            if (k%2)
                result.push_back(*midIterator);
            else
                result.push_back((*midIterator + *prev(midIterator))/2);

            if (i == nums.size())
                break;

            window.insert(nums[i]);
            if (nums[i] < *midIterator)
                midIterator--;
            if (nums[i-k] <= *midIterator)
                midIterator++;

            auto pos = window.find(nums[i-k]);
            window.erase(pos);
        }

        return result;
    }
};
```

