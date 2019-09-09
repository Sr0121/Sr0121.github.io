---
title: 'LeetCode:202. Happy Number'
date: 2019-06-20 20:31:43
categories: LeetCode
tags:
  - Python
  - LeetCode
---

**题目描述**

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example:** 

```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

<!--more-->

快乐数就是将自己的每一位数字的平方加起来后，最终为1的数字，如果中间出现了循环，则它不是快乐数。

所以需要用一个list存放所有在计算中出现的数字，如果原数字在进行计算的时候，出现了list中的数字，则不是快乐数。

**代码实现**

```python
class Solution:
    def isHappy(self, n: 'int') -> 'bool':
        if n <= 0:
            return False

        ns = []
        while n is not 1:
            next_n = 0
            if n in ns:
                return False
            ns.append(n)

            while n > 0:
                next_n += (n % 10)**2
                n = n // 10

            n = next_n

        return True

```

