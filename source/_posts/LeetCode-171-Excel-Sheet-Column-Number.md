---
title: 'LeetCode:171. Excel Sheet Column Number'
date: 2019-06-16 22:00:49
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```

**Example 1:**

```
Input: "A"
Output: 1
```

**Example 2:**

```
Input: "AB"
Output: 28
```

**Example 3:**

```
Input: "ZY"
Output: 701
```

<!--more-->

进制转换的题目

**代码实现**

```python
class Solution:
    def titleToNumber(self, s: 'str') -> 'int':
        result = 0
        for i in range(len(s)):
            result *= 26
            result += ord(s[i]) - 64

        return result

```

