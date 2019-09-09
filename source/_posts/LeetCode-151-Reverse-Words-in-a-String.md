---
title: 'LeetCode:151. Reverse Words in a String'
date: 2019-06-11 15:02:47
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Given an input string, reverse the string word by word.

 

**Example 1:**

```
Input: "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**

```
Input: "  hello world!  "
Output: "world! hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input: "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

 

**Note:**

- A word is defined as a sequence of non-space characters.
- Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
- You need to reduce multiple spaces between two words to a single space in the reversed string.

<!--more-->

本题用python实现的话其实挺简单的，直接用strip和split方法就可以

**代码实现**

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        s = s.strip()
        s_list = s.split(" ")
        result = ""
        for i in range(len(s_list)-1, -1, -1):
            if s_list[i] == "":
                continue
            result += " "+s_list[i]

        return result[1:]

```

