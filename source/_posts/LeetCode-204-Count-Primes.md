---
title: 'LeetCode:204. Count Primes'
date: 2019-06-23 10:02:00
categories: LeetCode
tags:
  - Python
  - LeetCode
---

**题目描述**

Count the number of prime numbers less than a non-negative number, **n**.

**Example:**

```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

<!--more-->

![img](https://leetcode.com/static/images/solutions/Sieve_of_Eratosthenes_animation.gif)

以n为121为例。本题的思想就是用数组的方法，先找2的倍数，把所有2的倍数（不包括2）进行标记。然后找接下来一个最小的没有被标记的数（3），将其倍数（不包括3）也标记起来。依此类推，一直做到11（根号121）为止。这是因为任何小于121的合数，必然会有一个因数小于11。

最后，数出没有被标记的数字的个数，就是小于121的质数的个数。

**代码实现**

```python
class Solution:
    def countPrimes(self, n: 'int') -> 'int':
        if n < 3:
            return 0

        isCount = [0] * n
        count = 0
        for i in range(2, int(math.sqrt(n-1))+1):
            if isCount[i] == 0:
                index = i
                while index+i < n:
                    index += i
                    isCount[index] = 1

        for i in range(2, n):
            if isCount[i] == 0:
                count += 1

        return count
```

