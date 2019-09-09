---
title: 'LeetCode: 295. Find Median from Data Stream'
date: 2019-09-06 21:00:19
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

For example,

```
[2,3,4]`, the median is `3
[2,3]`, the median is `(2 + 3) / 2 = 2.5
```

Design a data structure that supports the following two operations:

- void addNum(int num) - Add a integer number from the data stream to the data structure.
- double findMedian() - Return the median of all elements so far.

 

**Example:**

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

<!--more-->



Hard题。

如果是去使用quick sort维护数组，那么addNum的复杂度为O(nlogn)，查找为O(1)。

但是，这里可以使用一个最大堆存放整个stream的最小的一半数字，用最小堆存放整个stream的最大的一半数字，那么addNum的复杂度就是O(logn)，查找为O(1)，可以极大程度提升性能。

这里要注意的就是如何去维护两个堆中的数字。所以需要对每次addNum的数字与堆顶的数字进行比较和操作。比较简单，在此不加赘述。

**代码实现**

```python
import heapq

class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.minheap = []
        self.maxheap = []

    def addNum(self, num: int) -> None:
        if (len(self.minheap) + len(self.maxheap)) & 1:
            if num < self.minheap[0]:
                heapq.heappush(self.maxheap, -num)
            else:
                heapq.heappush(self.minheap, num)
                top = heapq.heappop(self.minheap)
                heapq.heappush(self.maxheap, -top)
        else:
            if len(self.maxheap) > 0 and num < -self.maxheap[0]:
                top = -heapq.heappop(self.maxheap)
                heapq.heappush(self.minheap, top)
                heapq.heappush(self.maxheap, -num)
            else:
                heapq.heappush(self.minheap, num)

    def findMedian(self) -> float:
        if (len(self.minheap) + len(self.maxheap)) & 1:
            return self.minheap[0]
        else:
            return (self.minheap[0] - self.maxheap[0])/2
```

