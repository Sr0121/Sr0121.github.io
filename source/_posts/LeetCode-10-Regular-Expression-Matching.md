---
title: 'LeetCode:10. Regular Expression Matching'
date: 2019-08-31 21:58:15
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an input string (`s`) and a pattern (`p`), implement regular expression matching with support for `'.'` and `'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the **entire** input string (not partial).

**Note:**

- `s` could be empty and contains only lowercase letters `a-z`.
- `p` could be empty and contains only lowercase letters `a-z`, and characters like `.` or `*`.

**Example 1:**

```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

**Example 2:**

```
Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

**Example 3:**

```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

**Example 4:**

```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
```

**Example 5:**

```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

<!--more-->



决定每天复习一下没有写在博客里的旧题hhh



这一题是一道hard的字符串匹配，难点在于匹配'*'。这里的\*代表任意个跟随着的字符，比如说A\*可以匹配"", "A", "AA", "AAA"。

总体的算法以递归实现。可以想象s和p各自有一个从0开始的index，称为index1和index2，他们会对s和p进行从左到右的匹配，如果说两个索引都走到了各自字符串的头的时候，就说明匹配完成。

当p[index2+1]不为'*'时，s[index1] == p[index2]（或p[index2]为'.'）的时候，s和p在各自的index上匹配，index1和index2个字加1，进行下一次匹配

当p[index2+1]为'*'的时候，可以匹配s[index1] == p[index2]（或p[index2]为'.'），或者说匹配s[index1] == p[index2+2]（此时跳过匹配p[index2]，'\*'对应s中的空白字符）

当index1走到s的头的时候，我们需要确定index2是否走到头，如果index2走到了头，则匹配成功，如果没有走到头，则要确定p中index2开始的子字符串都是由一个普通字符和一个'\*'交替组成的，如"A\*\.\*C\*"，如果是这样的话也是匹配成功，反之失败。

当index2走到p的头的时候，直接判断index1是否走到头，如果走到了就匹配成功。



具体实现方面，并没有用到index1和index2，而是在调用的时候使用了诸如s[1:]来表示index1+1的操作，并且每次仅比较s和p的index为0的字符。这样可以简化写法。



**代码实现**

```python
class Solution:
    def allStar(self, p):
        if len(p) % 2 == 1:
            return False

        for i in range(1, len(p), 2):
            if p[i] != '*':
                return False
        return True

    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        if len(p) == 0:
            if len(s) == 0:
                return True
            else:
                return False

        if len(s) == 0:
            return self.allStar(p)

        if len(p) > 1 and p[1] == '*':
            return (p[0] in [s[0], '.'] and self.isMatch(s[1:], p)) or self.isMatch(s, p[2:])
        elif s[0] == p[0] or p[0] == '.':
            return self.isMatch(s[1:], p[1:])
        else:
            return False

```

