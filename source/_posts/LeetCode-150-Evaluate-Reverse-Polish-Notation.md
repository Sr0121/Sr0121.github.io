---
title: 'LeetCode:150. Evaluate Reverse Polish Notation'
date: 2019-06-10 22:28:57
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, `/`. Each operand may be an integer or another expression.

**Note:**

- Division between two integers should truncate toward zero.
- The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.

**Example 1:**

```
Input: ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**

```
Input: ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

**Example 3:**

```
Input: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```


<!--more-->

本题就是要实现一个简单的stack，当输入为数字的时候进行push操作，对于操作符则需要pop出两个数字，并且进行计算，最后返回stack中的唯一元素即可。

**代码实现**

```python
class Solution(object):
    def evalRPN(self, tokens):
        """
        :type tokens: List[str]
        :rtype: int
        """
        stack = []
        for item in tokens:
            if item == "+":
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(num1+num2)
            elif item == "-":
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(num2-num1)
            elif item == "*":
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(num1*num2)
            elif item == "/":
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(int(num2/num1))
            else:
                stack.append(int(item))

        return stack[0]


```

