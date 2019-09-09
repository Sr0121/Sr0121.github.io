---
title: 'LeetCode:206. Reverse Linked List'
date: 2019-06-23 20:19:08
categories: LeetCode
tags:
  - Python
  - LeetCode
---

**题目描述**

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

<!--more-->

用一个虚的头节点（如下的start节点）可以简化代码。

**代码实现**

```python
class Solution:
    def reverseList(self, head: 'ListNode') -> 'ListNode':
        if head == None:
            return head
        start = ListNode(0)
        start.next = head
        tmp = head
        last = start
        while tmp != None:
            nextTmp = tmp.next
            tmp.next = last
            last = tmp
            tmp = nextTmp

        head.next = None
        return last
```

