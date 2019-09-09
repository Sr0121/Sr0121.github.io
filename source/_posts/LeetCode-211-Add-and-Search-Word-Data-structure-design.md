---
title: 'LeetCode:211. Add and Search Word - Data structure design'
date: 2019-06-25 20:59:44
categories: LeetCode
tags:
  - Python
  - LeetCode
---

**题目描述**

Design a data structure that supports the following two operations:

```
void addWord(word)
bool search(word)
```

search(word) can search a literal word or a regular expression string containing only letters `a-z` or `.`. A `.` means it can represent any one letter.

**Example:**

```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```


<!--more-->

本题就是要实现一个数据结构，可以进行增加字符串和查找功能，这里的查找功能可以是模糊查找。

本题的数据结构与之前的Trie一致，但是查找方面不同。这里的查找使用DFS，如果出现要匹配'.'，则需要在所有的子树上进行查找，任意子树返回True，则为匹配成功。

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = []
        self.end = False

class WordDictionary:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.start = Node(-1)

    def addWord(self, word: str) -> None:
        """
        Adds a word into the data structure.
        """
        this = self.start
        index = 0

        while index < len(word):
            find = False
            for i in this.next:
                if i.val == word[index]:
                    find = True
                    this = i
                    index += 1
                    break
            if find == False:
                newNode = Node(word[index])
                this.next.append(newNode)
                this = newNode
                index += 1

        this.end = True

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        """
        return self.dfs(word, self.start, 0)

    def dfs(self, word, node, index):
        if index == len(word):
            return node.end

        if word[index] == '.':
            for i in node.next:
                if self.dfs(word, i, index+1):
                    return True
            return False

        else:
            for i in node.next:
                if i.val == word[index] and self.dfs(word, i, index+1):
                    return True
            return False


```

