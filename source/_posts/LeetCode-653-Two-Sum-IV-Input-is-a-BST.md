---
title: 'LeetCode: 653. Two Sum IV - Input is a BST'
date: 2019-09-07 13:45:46
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

**Example 1:**

```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 9

Output: True
```

 

**Example 2:**

```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 28

Output: False
```

<!--more-->



使用中序遍历整个数，可以得到BST所有元素的从小到大的排列的list，然后对有序list找两个和为target。

对数组的操作比较简单，设置两个index，为数组的最左边和最右边的index，然后把两个元素加起来，如果和大于target，就右边index-=1，小于target就左边index+=1，直到和为target，返回True，或者左边的index大于右边index，返回False。

**代码实现**

```python
class Solution:
    def findTarget(self, root: TreeNode, k: int) -> bool:
        def dfs(root):
            if root == None:
                return
            dfs(root.left)
            allNums.append(root.val)
            dfs(root.right)

        allNums = []
        dfs(root)
        leftIndex = 0
        rightIndex = len(allNums) - 1
        while leftIndex < rightIndex:
            if allNums[leftIndex] + allNums[rightIndex] < k:
                leftIndex += 1
            elif allNums[leftIndex] + allNums[rightIndex] > k:
                rightIndex -= 1
            else:
                return True

        return False
```

