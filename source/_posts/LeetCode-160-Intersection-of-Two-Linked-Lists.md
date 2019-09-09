---
title: 'LeetCode:160. Intersection of Two Linked Lists'
date: 2019-06-12 23:13:54
categories: LeetCode
tags: 
  - LeetCode
  - C++
---

**题目概述**

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

![img](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)

begin to intersect at node c1.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

 

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```
Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Reference of the node with value = 2
Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

 

**Example 3:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

 

**Notes:**

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.


<!--more-->

本题的思路就是对两个链表进行从头到尾的遍历，并且将所得的地址存在两个vector中，然后从后往前比较vector，找到第一个不同的地址的索引，该索引+1就是两个链表的交点地址。

**代码实现**

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        vector<struct ListNode *> vector1;
        vector<struct ListNode *> vector2;

        while (headA != nullptr){
            vector1.push_back(headA);
            headA = headA->next;
        }

        vector1.push_back(nullptr);

        while (headB != nullptr){
            vector2.push_back(headB);
            headB = headB->next;
        }

        vector2.push_back(nullptr);

        int i = 1;
        int maxNum = vector1.size() > vector2.size()? vector2.size(): vector1.size();

        for (i = 1; i <= maxNum; i++){
            if (vector1[vector1.size()-i] != vector2[vector2.size()-i]){
                break;
            }
        }

        return vector1[vector1.size()-i+1];
    }
};
```

