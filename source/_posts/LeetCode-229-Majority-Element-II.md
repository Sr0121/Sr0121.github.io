---
title: 'LeetCode: 229. Majority Element II'
date: 2019-09-03 22:58:52
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an integer array of size *n*, find all elements that appear more than `⌊ n/3 ⌋` times.

**Note:** The algorithm should run in linear time and in O(1) space.

**Example 1:**

```
Input: [3,2,3]
Output: [3]
```

**Example 2:**

```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```

<!--more-->



如果要满足O(1)的space complexity的话，这是挺难的一道题。

由于需要找的数字最多只有两个，我们设置两个计数器，分别记录最有可能返回的两个值，以及他们记数的大小。

在遍历的时候，如果遍历到除了这两个数字之外的其他数字，就给他们两个的记述器都减1，如果遍历到与这两个数字相同的数字，就给相同的那个计数器加1.当某个计数器为0的时候，下一次遍历就可以将该计数器所对应的数字记为该新数字。

之所以这样做，是因为我们只需要记录最有可能的数字，如果说遍历到中途，某个数字的计数器变成0了，就说明它在当前的序列里，占比不会超过1/3，所以它一定不可能。

关于这题的理解我也并不是很透彻，已经标注了star

**代码实现**

```python
class Solution:
    def majorityElement(self, nums: 'list[int]') -> 'list[int]':
        num1, num2 = 0, 0
        count1, count2 = 0, 0
        threshold = len(nums) // 3

        for num in nums:
            if num1 == num:
                count1 += 1
            elif num2 == num:
                count2 += 1
            elif count1 == 0:
                num1 = num
                count1 = 1
            elif count2 == 0:
                num2 = num
                count2 = 1
            else:
                count1 -= 1
                count2 -= 1

        count1, count2 = 0, 0

        for num in nums:
            if num == num1:
                count1 += 1
            if num == num2:
                count2 += 1

        result = []
        if count1 > threshold:
            result.append(num1)
        if num2 != num1 and count2 > threshold:
            result.append(num2)

        return result
```

