---
title: 'LeetCode:179. Largest Number'
date: 2019-08-20 11:26:05
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a list of non negative integers, arrange them such that they form the largest number.

**Example 1:**

```
Input: [10,2]
Output: "210"
```

**Example 2:**

```
Input: [3,30,34,5,9]
Output: "9534330"
```

<!--more-->

题目要求对一串数组进行重新排列，让他们组合成最大的数字。比如[10,2]排列成"210"，[3,30,34,5,9]排列成"9534330"。

我们需要对每个字符的位数依次比较，比如[3,30,34,5,9]，第一位最大的是9，那么9就一定排在第一个，第一位第二大的是5，那么5就排在第二个，第三大的是3，然后就比第二位，于是第三个数字就是34...事实上，对于字符串a和b来说，如果a+b大于b+a，那么在最终排列的时候，a一定排在b的前面。

因此只需要实现一个compare函数，利用python内置的sort进行快排，就可以很快地得到我们需要的排序结果。最后注意要删除最左边的"0"，以及确保字符串不为空

**代码实现**

```python
from functools import cmp_to_key

class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        def compare(x, y):
            if int(str(x)+str(y)) > int(str(y)+str(x)):
                return 1
            elif int(str(x)+str(y)) < int(str(y)+str(x)):
                return -1
            else:
                return 0
        
        nums = sorted(nums, key=cmp_to_key(compare))
        
        result = ""
        for i in range(len(nums)-1, -1, -1):
            result += str(nums[i])
        
        result = result.lstrip("0")
        result = "0" if result == "" else result
        
        return result
```

