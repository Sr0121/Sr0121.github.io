---
title: 'LeetCode: 227. Basic Calculator II'
date: 2019-09-01 12:09:00
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only **non-negative** integers, `+`, `-`, `*`, `/` operators and empty spaces ``. The integer division should truncate toward zero.

**Example 1:**

```
Input: "3+2*2"
Output: 7
```

**Example 2:**

```
Input: " 3/2 "
Output: 1
```

**Example 3:**

```
Input: " 3+5 / 2 "
Output: 5
```

**Note:**

- You may assume that the given expression is always valid.
- **Do not** use the `eval` built-in library function.

<!--more-->



与之前的Basic Calculator一样，难点在于如何处理运算的优先级。但是与之前的括号不同，*和/仅仅是一个二元运算符，所以这题不需要使用递归，而只需要一个栈就可以了。

首先需要对字符串进行处理和分割，大致步骤与Basic Calculator一致，得到经过处理后的数字和操作符组成的数组newList，比如" 3+5 / 2"经过处理后得到['3', '+', '5', '/', '2']。

初始的stack为newList[0]，接下来，我们需要从头到尾对数组进行遍历。当遍历到'+'，则直接push进下一个元素，当遍历到'-'的时候，push进下一个元素的相反数，当遍历到'*'和'/'的时候，需要pop出栈顶元素后，与下一个元素进行乘法或除法的操作后，将结果push进stack。最后，将stack的所有元素相加，得到最终结果。

纵观全过程，我们是在遍历到乘号或除号的时候直接对数字进行操作，而最后对stack的所有元素相加则为对加减法的统一操作。因此可以实现乘除法的优先级大于加减法的操作。

**代码实现**

```python
class Solution:
    def calculate(self, s: str) -> int:
        s = s.replace(" ","")
        s = s.replace("+", " + ")
        s = s.replace("-", " - ")
        s = s.replace("*", " * ")
        s = s.replace("/", " / ")
        s = s.strip()
        sList = s.split(" ")
        filterList = filter(lambda x: x != "", sList)
        newList = list(filterList)

        stack = [int(newList[0])]
        i = 1
        while i < len(newList):
            if newList[i] == '+':
                i += 1
                stack.append(int(newList[i]))
            elif newList[i] == '-':
                i += 1
                stack.append(-int(newList[i]))
            elif newList[i] == '*':
                i += 1
                last = stack.pop()
                stack.append(last * int(newList[i]))
            elif newList[i] == '/':
                i += 1
                last = stack.pop()
                stack.append(int(last / int(newList[i])))
            else:
                assert 0

            i += 1

        return sum(stack)

```

