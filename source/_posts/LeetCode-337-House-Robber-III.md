---
title: 'LeetCode: 337. House Robber III'
date: 2019-09-08 15:36:45
categories: LeetCode
tags:
  - LeetCode
  - C++
---

**题目描述**

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example 1:**

```
Input: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

Output: 7 
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

**Example 2:**

```
Input: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```

<!--more-->



这题是小偷的第三题，前两题因为都是一个数列，所以很容易就可以用DP做。

但是这题所有的路线是用二叉树来表示的，因此首选思路还是DFS。

对于每一个节点，它的偷窃的最大值只有两种情况，第一种是自己的两个子节点们的返回值之和，还有一种是自己的值加上自己的孙子节点们的返回值之和，所以dfs还是比较好实现的。

有一点要注意的是，需要用一个hashMap来存储每个节点的返回值，因为在进行dfs的时候，会重复查找节点的值，如果没有一个hashMap来存储数据的话，会TLE。

**代码实现**

```c++
class Solution {
private:
    unordered_map<TreeNode*, int> hashMap;
    int subTreeRob(TreeNode* root) {
        if (root == NULL) {
            return 0;
        }
        if (hashMap.find(root) != hashMap.end()){
            return hashMap[root];
        }

        int result = 0;
        if (root->left != NULL && root->right != NULL) {
            result = max(root->val + subTreeRob(root->left->left) + subTreeRob(root->left->right) + subTreeRob(root->right->left) + subTreeRob(root->right->right), subTreeRob(root->left) + subTreeRob(root->right));
        }
        else if (root->left != NULL) {
            result = max(root->val + subTreeRob(root->left->left) + subTreeRob(root->left->right), subTreeRob(root->left));
        }
        else if (root->right != NULL){
            result = max(root->val + subTreeRob(root->right->left) + subTreeRob(root->right->right), subTreeRob(root->right));
        }
        else {
            result = root->val;
        }
        hashMap[root] = result;
        return result;
    }
public:
    int rob(TreeNode* root) {
        return subTreeRob(root);
    }
};
```

