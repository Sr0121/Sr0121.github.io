---
title: 'LeetCode:226. Invert Binary Tree'
date: 2019-09-01 11:36:48
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Invert a binary tree.

**Example:**

Input:

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

<!--more-->



本题就是让我们反转一下二叉树，左右子树进行对调。可以使用一个递归实现。

```python
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if root == None:
            return root
        tmp = root.left
        root.left = root.right
        root.right = tmp
        if root.left:
            self.invertTree(root.left)
        if root.right:
            self.invertTree(root.right)
        return root
```

