---
title: 'LeetCode: 445. Add Two Numbers II'
date: 2019-09-07 16:59:10
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

<!--more-->



这里需要对两个链表进行加法，首先需要将列表进行反转，然后从表头进行链表的遍历。然后对两个链表进行同时从头到尾遍历。每一次遍历后将值相加，然后保存到一个新的节点中，然后两个节点都向后移一位。最后要注意两个表都遍历到头了以后，如果carry为1，还需要额外生成一个节点连接到结果的最后。

在返回前，需要对结果再进行一次反转。

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        def reverseList(l:'ListNode') -> 'ListNode':
            if l == None:
                return l
            lastNode = None
            while l.next != None:
                nextL = l.next
                l.next = lastNode
                lastNode = l
                l = nextL
            l.next = lastNode
            return l

        reversedL1 = reverseList(l1)
        reversedL2 = reverseList(l2)
        start = ListNode(0)
        last = start
        carry = 0
        while reversedL1 != None or reversedL2 != None:
            val1 = 0 if reversedL1 == None else reversedL1.val
            val2 = 0 if reversedL2 == None else reversedL2.val

            val = val1 + val2 + carry
            carry = val // 10
            val = val % 10

            last.next = ListNode(val)
            last = last.next
            reversedL1 = None if reversedL1 == None else reversedL1.next
            reversedL2 = None if reversedL2 == None else reversedL2.next
            
        if carry == 1:
            last.next = ListNode(1)

        return reverseList(start.next)
```

