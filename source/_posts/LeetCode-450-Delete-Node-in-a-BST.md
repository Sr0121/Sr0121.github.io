---
title: 'LeetCode: 450. Delete Node in a BST'
date: 2019-09-07 15:20:33
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.



**Note:** Time complexity should be O(height of tree).

**Example:**

```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```

<!--more-->



这题需要在二分查找树中删除节点。

在找到该节点位置之后，二分查找树删除节点的思路为：

* 如果该节点没有子节点，则直接删除
* 如果该节点有左子节点，就找左子树的最大值替换该节点的值，并且删除左子树中的最大节点
* 如果该节点有右子节点，就找右子树的最小值替换该节点的值，并且删除右子树中的最小节点

我使用了循环而非递归来做，所以代码看起来会比较繁琐，但是效率会比递归的更高。

**代码实现**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:

        """
        :type root: TreeNode
        :type key: int
        :rtype: TreeNode
        """
        if root == None:
            return root

        node = root
        lastNode = None
        while node.val != key:
            if node.val > key and node.left != None:
                lastNode = node
                node = node.left
            elif node.val < key and node.right != None:
                lastNode = node
                node = node.right
            else:
                break

        if node.val != key:
            return root

        if node.left == None and node.right == None:
            if lastNode == None:
                return None
            if lastNode.left != None and lastNode.left.val == key:
                lastNode.left = None
            else:
                lastNode.right = None

        elif node.left != None:
            leftMax = node.left
            leftMaxLast = node
            while leftMax.right != None:
                leftMaxLast = leftMax
                leftMax = leftMax.right
            if leftMaxLast != node:
                leftMaxLast.right = leftMax.left
            else:
                leftMaxLast.left = leftMax.left
            node.val = leftMax.val

        else:
            rightMin = node.right
            rightMinLast = node
            while rightMin.left != None:
                rightMinLast = rightMin
                rightMin = rightMin.left
            if rightMinLast != node:
                rightMinLast.left = rightMin.right
            else:
                rightMinLast.right = rightMin.right
            node.val = rightMin.val

        return root

```

