---
title: 'LeetCode:205. Isomorphic Strings'
date: 2019-06-23 10:25:24
categories: LeetCode
tags:
  - Python
  - LeetCode
---

**题目描述**

Given two strings **s** and **t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in **s** can be replaced to get **t**.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

**Example 1:**

```
Input: s = "egg", t = "add"
Output: true
```

**Example 2:**

```
Input: s = "foo", t = "bar"
Output: false
```

**Example 3:**

```
Input: s = "paper", t = "title"
Output: true
```


<!--more-->

用了一个字符串，按顺序存放s和t的索引上的字母首次出现的位置，最后比较这两个位置是否相同。

**代码实现**

```python
class Solution:
    def isIsomorphic(self, s: 'str', t: 'str') -> 'bool':
        mapS = {}
        mapT = {}
        indexS = ""
        indexT = ""

        for i in range(len(s)):
            if s[i] not in mapS.keys():
                mapS[s[i]] = i
                indexS += str(i)
            else:
                indexS += str(mapS[s[i]])

        for i in range(len(t)):
            if t[i] not in mapT.keys():
                mapT[t[i]] = i
                indexT += str(i)
            else:
                indexT += str(mapT[t[i]])

        if indexS == indexT:
            return True
        else:
            return False
```

