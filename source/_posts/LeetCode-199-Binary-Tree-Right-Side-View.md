---
title: 'LeetCode:199. Binary Tree Right Side View'
date: 2019-06-19 17:02:50
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given a binary tree, imagine yourself standing on the *right* side of it, return the values of the nodes you can see ordered from top to bottom.

**Example:**

```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

<!--more-->

这题很像之前的按照行来对树进行遍历，就是用一个类似先用一个queue来存放头节点，对queue中的所有元素的left和right进行检查，如果不是None的话就存放到另一个tmp_queue中，直到遍历完queue中的所有元素为止。接着把tmp_queue赋值给queue，进行新的一层的遍历。

所以只需要记录每一次的tmp_queue的最后一个元素即可。

**代码实现**

```python
class Solution:
    def rightSideView(self, root: 'TreeNode') -> 'list[int]':
        result = []
        if root == None:
            return result
        queue = [root]
        result.append(root.val)

        while len(queue) > 0:
            tmp = []
            for i in queue:
                if i.left != None:
                    tmp.append(i.left)
                if i.right != None:
                    tmp.append(i.right)
            if len(tmp) > 0:
                result.append(tmp[-1].val)
            queue = tmp

        return result
```

