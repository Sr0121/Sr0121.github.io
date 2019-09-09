---
title: 'LeetCode:168. Excel Sheet Column Title'
date: 2019-06-16 21:23:17
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```

**Example 1:**

```
Input: 1
Output: "A"
```

**Example 2:**

```
Input: 28
Output: "AB"
```

**Example 3:**

```
Input: 701
Output: "ZY"
```

<!--more-->

进制转换的题目

**代码实现**

```python
class Solution:
    def convertToTitle(self, n: 'int') -> 'str':
        result = ""
        while True:
            remainder = (n-1) % 26
            n = int((n-1)/26)
            result = chr(65+remainder) + result
            if n == 0:
                break

        return result
```

