---
title: 'LeetCode:167. Two Sum II - Input array is sorted'
date: 2019-06-15 22:48:25
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given an array of integers that is already **sorted in ascending order**, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

- Your returned answers (both index1 and index2) are not zero-based.
- You may assume that each input would have *exactly* one solution and you may not use the *same* element twice.

**Example:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```


<!--more-->

简单题，由于数组是递增的，所以一开始假定index1为0，index2为数组的最后一个索引，如果对应的两个数相加比target小，则让index1加一，反之让index2减1，直到找到两个和为target的值的索引

最后注意把求得的index+1即可。

**代码实现**

```python
class Solution:
    def twoSum(self, numbers: 'list[int]', target: 'int') -> 'list[int]':
        index1 = 0
        index2 = len(numbers) - 1

        while numbers[index1] + numbers[index2] != target:
            if numbers[index1] + numbers[index2] > target:
                index2 -= 1
            else:
                index1 += 1

        return [index1+1, index2+1]

```

