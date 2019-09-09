---
title: 'LeetCode:148. Sort List'
date: 2019-06-09 16:36:05
categories: LeetCode
tags: 
  - LeetCode
  - C++
---

**题目概述**

Sort a linked list in *O*(*n* log *n*) time using constant space complexity.

**Example 1:**

```
Input: 4->2->1->3
Output: 1->2->3->4
```

**Example 2:**

```
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```

<!--more-->

这是一道挺好的题目，第一眼给人的感觉非常简单，就是实现一个快速排序。但是实际上，链表的快速排序和数组的快速排序差别还是很大的。其中最重要的地方就是要在实现递归的快速排序的同时，保证链表的完整性，即所有Nodes需要传成一条链，并且保证你能访问到这条链的头节点。这就需要实现快速排序的方法能够将头节点进行传出。



**代码实现**

```c++
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        return this->quickSort(head, nullptr);
    }

private:
    ListNode* quickSort(ListNode* start, ListNode* end){
        if (start == nullptr){
            return nullptr;
        }

        int standard = start->val;
        ListNode* leftStart = new ListNode(-1);
        ListNode* leftTail = leftStart;
        ListNode* rightStart = new ListNode(-1);
        ListNode* rightTail = rightStart;
        ListNode* checkNode = start->next;
        while (checkNode != end){
            if (checkNode->val <= standard){
                leftTail->next = checkNode;
                leftTail = leftTail->next;
            } else {
                rightTail->next = checkNode;
                rightTail = rightTail->next;
            }
            ListNode* saveCheckNode = checkNode;
            checkNode = checkNode->next;
            saveCheckNode->next = nullptr;
        }
        leftStart->next = this->quickSort(leftStart->next, end);
        rightStart->next = this->quickSort(rightStart->next, end);
        leftTail = leftStart;
        while (leftTail->next != nullptr){
            leftTail = leftTail->next;
        }
        leftTail->next = start;
        start->next = rightStart->next;

        return leftStart->next;
    }
};
```

