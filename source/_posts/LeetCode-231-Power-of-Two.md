---
title: 'LeetCode: 231. Power of Two'
date: 2019-09-04 13:38:07
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an integer, write a function to determine if it is a power of two.

**Example 1:**

```
Input: 1
Output: true 
Explanation: 20 = 1
```

**Example 2:**

```
Input: 16
Output: true
Explanation: 24 = 16
```

**Example 3:**

```
Input: 218
Output: false
```

<!--more-->



所有2的n次方的数字的二进制表示中，只有一个1，并且该1出现在首位。

因此，该题目就是判断输入的数字的二进制表示中有几个1，如果出现了多个1，那就一定不对。在实现方面，我使用了位运算，不断对输入向右移位，直到出现第一个1为止。这个时候进行判断，如果该数字仍然大于1，则说明这个数字还包含了多个1，因此返回false。另外需要排除0和一切负数的情况。

```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        if n < 1:
            return False

        while n > 0:
            if n & 1 == 1:
                break
            n >>= 1

        if n > 1:
            return False
        return True

```

