---
title: 'LeetCode:225. Implement Stack using Queues'
date: 2019-09-01 11:31:13
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Implement the following operations of a stack using queues.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- empty() -- Return whether the stack is empty.

**Example:**

```
MyStack stack = new MyStack();

stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false
```

**Notes:**

- You must use *only* standard operations of a queue -- which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.
- Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
- You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

<!--more-->



**代码实现**

```python
class MyStack:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack = []

    def push(self, x: int) -> None:
        """
        Push element x onto stack.
        """
        self.stack.append(x)

    def pop(self) -> int:
        """
        Removes the element on top of the stack and returns that element.
        """
        return self.stack.pop()

    def top(self) -> int:
        """
        Get the top element.
        """
        return self.stack[-1]

    def empty(self) -> bool:
        """
        Returns whether the stack is empty.
        """
        return True if len(self.stack) == 0 else False
```

