---
title: 'LeetCode:147. Insertion Sort List'
date: 2019-06-09 13:37:06
categories: LeetCode
tags: 
  - LeetCode
  - C++
---

**题目概述**

<table><tr><td bgcolor=#EDEDED>Sort a linked list using insertion sort.
A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.
With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list
</td></tr></table>

![img](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)

<!--more-->

本题本质上是一个水题，就是简单的插入排序，只是使用了链表来进行处理。只需要将普通的数组插入排序对数组的遍历操作改成对链表的遍历即可。



```c++
class Solution {
public:
    ListNode* insertionSortList(ListNode* head) {
        if (head == nullptr)
            return head;

        ListNode *ori = new ListNode(-2147483648);
        ori->next = head;
        ListNode *last = ori;
        ListNode *current = head;

        while (current != nullptr) {
            if (current->val >= last->val) {
                current = current->next;
                last = last->next;
            } else {
                ListNode *saveNext = current->next;
                ListNode *start = ori;
                while (start->next->val <= current->val)
                    start = start->next;
                current->next = start->next;
                start->next = current;
                last->next = saveNext;
                current = saveNext;
            }
        }
        last->next = nullptr;
        return ori->next;
    }
};
```

