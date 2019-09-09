---
title: 'LeetCode:203. Remove Linked List Elements'
date: 2019-06-20 22:30:17
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Remove all elements from a linked list of integers that have value **val**.

**Example:**

```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

<!--more-->

**代码实现**

```python
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        start = ListNode(0)
        start.next = head
        tmp = head
        last = start
        while tmp != None:
            if tmp.val == val:
                last.next = tmp.next
                tmp = tmp.next
            else:
                last = last.next
                tmp = tmp.next

        return start.next
```



