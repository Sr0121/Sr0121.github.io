---
title: 'LeetCode:166. Fraction to Recurring Decimal'
date: 2019-06-15 22:30:10
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

**Example 1:**

```
Input: numerator = 1, denominator = 2
Output: "0.5"
```

**Example 2:**

```
Input: numerator = 2, denominator = 1
Output: "2"
```

**Example 3:**

```
Input: numerator = 2, denominator = 3
Output: "0.(6)"
```


<!--more-->

本题的难点就在如何找到无限循环小数的循环体。

以5/3为例：5/3的整数部分为int(5/3)也就是1，余数为2，然后计算小数点1位之后的数字时，实际上是把2乘以了10，也就是20再除以3，得到了6，余2。这里的6就是小数点后1位的数字。接着，再用余数2*10/3...以此类推。所以说，我们只需要一个数组，存放每一次进行除法操作后的余数，如果余数相同，则已经开始循环了。

在实现的时候，我使用的是数组而不是哈希表，主要还是因为题目需要在结果字符串中添加括号，使用数组更容易对括号的地方进行定位。

**代码实现**

````python
class Solution:
    def fractionToDecimal(self, numerator: 'int', denominator: 'int') -> 'str':
        sign = 1 if numerator/denominator >= 0 else -1
        numerator = abs(numerator)
        denominator = abs(denominator)
        remainder = numerator % denominator
        if remainder == 0:
            return str(int(sign * numerator / denominator))

        result = "-" if sign == -1 else ""
        result += str(int(numerator/denominator))
        result += '.'

        remainderList = []

        while True:
            if remainder == 0:
                return result
            if remainder in remainderList:
                for i in range(len(remainderList)):
                    if remainderList[i] == remainder:
                        insertIndex = len(remainderList) - i
                        resultList = list(result)
                        resultList.insert(-insertIndex, '(')
                        resultList.append(')')
                        result = "".join(resultList)
                        return result
            else:
                remainderList.append(remainder)
                remainder *= 10
                result += str(int(remainder / denominator))
                remainder = remainder % denominator
````

