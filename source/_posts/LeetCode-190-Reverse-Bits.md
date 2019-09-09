---
title: 'LeetCode:190. Reverse Bits'
date: 2019-08-28 23:14:21
categories: LeetCode
tags:
  - LeetCode
  - C++
---

**题目描述**

Reverse bits of a given 32 bits unsigned integer.

 

**Example 1:**

```
Input: 00000010100101000001111010011100
Output: 00111001011110000010100101000000
```

**Example 2:**

```
Input: 11111111111111111111111111111101
Output: 10111111111111111111111111111111
```

<!--more-->



考查位运算，比较坑的点是位运算符的优先级相对于四则运算更低。

**代码实现**

```c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t result = 0;
            
        for (int i = 0; i < 32; i++) {
            result <<= 1;
            if (n & 1) {
                result += 1;
            }
            n >>= 1;
        }
        return result;
    }
};
```

