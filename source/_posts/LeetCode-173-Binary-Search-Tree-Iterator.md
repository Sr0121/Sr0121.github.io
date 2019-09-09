---
title: 'LeetCode:173. Binary Search Tree Iterator'
date: 2019-06-17 20:50:18
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目概述**

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling `next()` will return the next smallest number in the BST.

 



**Example:**

**![img](https://assets.leetcode.com/uploads/2018/12/25/bst-tree.png)**

```
BSTIterator iterator = new BSTIterator(root);
iterator.next();    // return 3
iterator.next();    // return 7
iterator.hasNext(); // return true
iterator.next();    // return 9
iterator.hasNext(); // return true
iterator.next();    // return 15
iterator.hasNext(); // return true
iterator.next();    // return 20
iterator.hasNext(); // return false
```

 

**Note:**

- `next()` and `hasNext()` should run in average O(1) time and uses O(*h*) memory, where *h* is the height of the tree.
- You may assume that `next()` call will always be valid, that is, there will be at least a next smallest number in the BST when `next()` is called.

<!--more-->

这题我使用了一个DFS来遍历BST，并且把按顺序把树的节点存到了self.nodes的list中。这个类同时还保存了一个当前对象在self.nodes的索引值，如果使用了next方法，就把这个索引值加一，hasnext则判断这个索引值和self.nodes的长度的关系

**代码实现**

```python
class BSTIterator:
    def __init__(self, root: TreeNode):
        self.nodes = []
        self.dfs(root)
        self.index = -1

    def next(self) -> int:
        """
        @return the next smallest number
        """
        self.index += 1
        return self.nodes[self.index].val

    def hasNext(self) -> bool:
        """
        @return whether we have a next smallest number
        """
        if self.index < len(self.nodes) - 1:
            return True
        else:
            return False

    def dfs(self, root):
        if root == None:
            return
        self.dfs(root.left)
        self.nodes.append(root)
        self.dfs(root.right)


```

