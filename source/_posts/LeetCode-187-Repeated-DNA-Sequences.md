---
title: 'LeetCode:187. Repeated DNA Sequences'
date: 2019-08-27 22:53:22
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

**Example:**

```
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"

Output: ["AAAAACCCCC", "CCCCCAAAAA"]
```

<!--more-->



创建两个set，第一个set用来存放结果，另一个set用来存放从头到尾遍历的字符长度为10的子字符串的结果。如果遍历到的字符串再第二个set中存在，就把它存放到第一个结果set中，否则就将它放到第二个set中。由于使用set，复杂度为O(n)，n为s的长度

**代码实现**

```python
class Solution:
    def findRepeatedDnaSequences(self, s: 'str') -> 'List[str]':
        nums = set()
        result = set()
        for i in range(len(s)-9):
            if s[i:i+10] in nums:
                result.add(s[i:i+10])
            else:
                nums.add(s[i:i+10])
        return list(result)
```

