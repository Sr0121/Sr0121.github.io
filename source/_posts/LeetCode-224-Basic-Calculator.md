---
title: 'LeetCode:224. Basic Calculator'
date: 2019-08-31 16:15:17
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, **non-negative**integers and empty spaces ``.

**Example 1:**

```
Input: "1 + 1"
Output: 2
```

**Example 2:**

```
Input: " 2-1 + 2 "
Output: 3
```

**Example 3:**

```
Input: "(1+(4+5+2)-3)+(6+8)"
Output: 23
```

Note:

- You may assume that the given expression is always valid.
- **Do not** use the `eval` built-in library function.

<!--more-->



这题需要实现一个简单的计算器，比较难的点在于如何处理括号。在对字符串进行处理后，根据'+', '-', '(', ')'作为分隔符，得到每一个数字和他们对应的运算符号，存在一个list里。

每次遇到'('的时候，就需要进行一次递归，在遇到')'的时候，从该层递归返回结果。

**代码实现**

```python
class Solution:
    def calculate(self, s: str) -> int:
        def tmpCalculation(index):
            tmp = 0
            sign = 1
            while index < len(newList):
                if newList[index] == '(':
                    returnResult, index = tmpCalculation(index + 1)
                    tmp = tmp + sign * returnResult
                elif newList[index] == ')':
                    return tmp, index
                elif newList[index] == '+':
                    sign = 1
                elif newList[index] == '-':
                    sign = -1
                else:
                    tmp = tmp + sign * int(newList[index])

                index += 1

            return tmp, index


        s = s.replace(" ", "")
        s = s.replace("+", " + ")
        s = s.replace("-", " - ")
        s = s.replace("(", " ( ")
        s = s.replace(")", " ) ")
        s = s.strip()
        sList = s.split(" ")
        filterList = filter(lambda x: x != "", sList)
        newList = list(filterList)
        result, _ = tmpCalculation(0)
        return result

```

