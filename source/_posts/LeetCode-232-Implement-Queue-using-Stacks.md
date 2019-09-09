---
title: 'LeetCode: 232. Implement Queue using Stacks'
date: 2019-09-08 12:43:33
categories: LeetCode
tags:
  - LeetCode
  - C++
---

**题目描述**

Implement the following operations of a queue using stacks.

- push(x) -- Push element x to the back of queue.
- pop() -- Removes the element from in front of queue.
- peek() -- Get the front element.
- empty() -- Return whether the queue is empty.

**Example:**

```
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false
```

**Notes:**

- You must use *only* standard operations of a stack -- which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
- Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
- You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

<!--more-->



使用stack模拟queue，对于peek和pop操作需要另外一个stack协助完成，原stack进行pop操作的时候另一个stack进行push来保存所有元素。

**代码实现**

```c++
class MyQueue {
private:
    stack<int> _stack;

public:
    /** Initialize your data structure here. */
    MyQueue() {

    }

    /** Push element x to the back of queue. */
    void push(int x) {
        this->_stack.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        stack<int> tmp;
        assert (!this->_stack.empty());
        int popNum = 0;
        while (!this->_stack.empty()) {
            popNum = this->_stack.top();
            this->_stack.pop();
            if (!this->_stack.empty()) {
                tmp.push(popNum);
            }
        }
        while (!tmp.empty()) {
            this->_stack.push(tmp.top());
            tmp.pop();
        }
        return popNum;
    }

    /** Get the front element. */
    int peek() {
        stack<int> tmp;
        int topNum = 0;
        while (!this->_stack.empty()) {
            tmp.push(this->_stack.top());
            this->_stack.pop();
        }
        topNum = tmp.top();
        while (!tmp.empty()) {
            this->push(tmp.top());
            tmp.pop();
        }
        return topNum;
    }

    /** Returns whether the queue is empty. */
    bool empty() {
        return this->_stack.empty();
    }
};

```

