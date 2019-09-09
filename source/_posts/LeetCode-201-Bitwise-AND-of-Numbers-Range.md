---
title: 'LeetCode:201. Bitwise AND of Numbers Range'
date: 2019-06-20 16:07:48
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

**Example 1:**

```
Input: [5,7]
Output: 4
```

**Example 2:**

```
Input: [0,1]
Output: 0
```

<!--more-->

这道题目需要找到连续范围内的所有数的与，如果直接进行与的话会导致超时。

当m和n位数不同的时候，比如说m是0b11, n是0b111，由于由于他们位数不同，那么他们中一定会出现一个0b100，与m在后两位上的与都是0，所以m和n在位数不同的情况下一定是0.

当位数相同的时候，比如说m为0b11001，n为0b11100的时候，他们之间有0b11010，0b11011，可以看出，他们这些数字的头两位都是一样的，而后几位的与都为0.

因此，本题也就是要求解m和n的二进制表达下的头几位是相同的。考虑到之前的m和n位数不同的时候，m的头几位可以用0来补足，因此之前的特殊情况也符合该描述。

**代码实现**

```python
class Solution:
    def rangeBitwiseAnd(self, m: 'int', n: 'int') -> 'int':
        tmp = n
        bits = 0
        if m == n:
            return m
        while tmp > 0:
            tmp = tmp >> 1
            bits = bits*2 + 1

        count = 1
        while bits & n != bits & m:
            bits = bits >> count
            bits = bits << count
            count += 1

        return bits & m

```

