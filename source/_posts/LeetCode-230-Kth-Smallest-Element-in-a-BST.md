---
title: 'LeetCode: 230. Kth Smallest Element in a BST'
date: 2019-09-04 13:25:52
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a binary search tree, write a function `kthSmallest` to find the **k**th smallest element in it.

**Note:** 
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Example 1:**

```
Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
```

**Example 2:**

```
Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
```

<!--more-->



由于这个是一个二叉搜索树，因此内部的数字已经排列好了，我们只需要通过遍历树去找到第k小的数字。

这里可以用中序遍历的方法，在遍历第k次的时候，该node的val就是所需要求解的值。

```python
class Solution:
    def __init__(self):
        self.tmp = 0
        self.k = 0
        self.result = 0

    def traversal(self, root):
        if root == None:
            return
        self.traversal(root.left)

        self.tmp += 1

        if self.tmp == self.k:
            self.result = root.val

        self.traversal(root.right)

    def kthSmallest(self, root: 'TreeNode', k: 'int') -> 'int':
        self.k = k
        self.traversal(root)
        return self.result
```

