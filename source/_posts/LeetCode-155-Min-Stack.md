---
title: 'LeetCode:155. Min Stack'
date: 2019-06-12 16:18:15
categories: LeetCode
tags:
  - C++
  - LeetCode
---

**题目概述**

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

 

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

<!--more-->

本题的解法就是要实现两个栈。其中一个栈用来存放原数据信息，第二个栈用来存放当前栈的最小值。第二个栈的栈顶是当前栈的最小值。在进行push和pop的时候，对第一个栈进行常规操作，当push的值小于第二个栈的栈顶时，要将该值也push进第二个栈；如果pop出的值为第二个栈的栈顶元素时，也需要对第二个栈进行pop操作。



**代码实现**

```c++
class MinStack {
private:
    stack<int> itemStack;
    stack<int> minStack;
public:
    /** initialize your data structure here. */
    MinStack() {
    }

    void push(int x) {
        if (minStack.empty() || minStack.top() >= x){
            itemStack.push(x);
            minStack.push(x);
        } else {
            itemStack.push(x);
        }
    }

    void pop() {
        if (itemStack.top() == minStack.top()){
            itemStack.pop();
            minStack.pop();
        } else {
            itemStack.pop();
        }
    }

    int top() {
        return itemStack.top();
    }

    int getMin() {
        return minStack.top();
    }
};
```

