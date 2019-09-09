---
title: 'LeetCode:212. Word Search II'
date: 2019-06-26 23:35:40
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

 

**Example:**

```
Input: 
board = [
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
words = ["oath","pea","eat","rain"]

Output: ["eat","oath"]
```

 

**Note:**

1. All inputs are consist of lowercase letters `a-z`.
2. The values of `words` are distinct.


<!--more-->

这题我一开始尝试暴力搜索，需要对所有字符串，board的长和宽都进行一次循环遍历。最后出了很多bug，而且超时。

后来查阅了网上的一些资料，才知道这题也要使用之前的Trie树来进行搜索。这样可以减少一层的循环。

所以一开始，需要把word里的所有字符串存到Trie中，然后对board中的所有元素依此进行深度优先搜索，查找当前的字符是否在Trie当前节点的子节点中，如果没有则直接返回，如果有，则让当前Trie的节点变为该子节点，然后查找当前字符的上下左右四个相邻的字符是否在新的Trie节点的子节点中，以此类推，实现一个深度优先搜索。如果当前节点是某个Trie中的字符串的结束字符，则将该字符串存入结果中，最终返回结果。

**代码实现**

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = [None] * 26
        self.end = False

class Trie:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.start = Node("")

    def insert(self, word: str) -> None:
        """
        Adds a word into the data structure.
        """
        this = self.start

        for i in range(len(word)):
            index = ord(word[i]) - ord('a')
            if this.next[index] == None:
                this.next[index] = Node(this.val + word[i])
            this = this.next[index]

        this.end = True


class Solution:
    def findWords(self, board: 'list[list[str]]', words: 'list[str]') -> 'list[str]':
        def dfs(root, x, y):
            if isVisited[x][y] == 1:
                return

            if root.end == True:
                result.append(root.val)
                root.end = False

            isVisited[x][y] = 1

            direct = [[0, 1], [1, 0], [0, -1], [-1, 0]]

            for dir in direct:
                newx = x + dir[0]
                newy = y + dir[1]
                if newx < 0 or newx >= len(board) or newy < 0 or newy >= len(board[0]):
                    continue
                if root.next[ord(board[newx][newy]) - ord('a')] != None:
                    dfs(root.next[ord(board[newx][newy]) - ord('a')], newx, newy)

            isVisited[x][y] = 0

        trie = Trie()
        for word in words:
            trie.insert(word)

        result = []
        if len(board) == 0 or len(board[0]) == 0:
            return result

        isVisited = [[0] * len(board[0]) for _ in range(len(board))]

        for i in range(len(board)):
            for j in range(len(board[0])):
                if trie.start.next[ord(board[i][j]) - ord('a')] != None:
                    dfs(trie.start.next[ord(board[i][j]) - ord('a')], i, j)

        return result

```

