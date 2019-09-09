---
title: 'LeetCode:222. Count Complete Tree Nodes'
date: 2019-08-29 23:25:27
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a **complete** binary tree, count the number of nodes.

**Note:** 

**Definition of a complete binary tree from Wikipedia:**
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

**Example:**

```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```

<!--more-->



**代码实现**

```
class Solution:
    def countNodes(self, root: TreeNode) -> int:
        result = 0
        if root == None:
            return 0
        
        nodes = [root]
        while len(nodes) > 0:
            tmp = nodes.pop(0)
            result += 1
            if tmp.left != None:
                nodes.append(tmp.left)
            if tmp.right != None:
                nodes.append(tmp.right)
                
        return result
```

