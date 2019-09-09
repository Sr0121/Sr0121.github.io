---
title: 'LeetCode: 239. Sliding Window Maximum'
date: 2019-09-06 19:55:01
categories: LeetCode
tags:
  - LeetCode
  - Python
---

**题目描述**

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

**Example:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

<!--more-->



Hard题，难点在于O(n)算法的实现。

这里的O(n)需要使用一个可以维持顺序的队列，成为单调队列。该队列中存储了最有可能成为Max的数字，比如对于k=3, nums=[2, 1, 4, 5]来说，一开始的这个队列长度为0，对nums进行从左到右遍历。首先先看第一个元素2，直接进入队列中，然后看第二个元素1，实际上1还是有可能成为Max的数字的，因为当2出列的时候，1就有可能成为最大的数字，因此push进1，单调队列为[2, 1]，接下来是4，由于4比单调队列中的所有数字都大，而且之前的数字出列之前，之前的数字都不可能再成为最大的数字了，因此把单调队列pop两次，再push进4。此时，第一个sliding window的最大值就是最左边的这个元素4。当遍历到5的时候，由于5比4大，而且之后4也不可能成为最大的了，所以就pop出4，push进5.

这里需要注意的就是要检查每一次出sliding window时出去的这个元素是不是单调队列中最大的那个元素，如果是的话，就要把最开头的这个元素pop掉；如果不是，则不用处理，因为它也一定不会存在于单调队列的其他地方中，也不会对之后的结果有任何影响。（这里可能就是hint所说的双向队列deque的体现吧）

**代码实现**

```python
class Solution:
    def maxSlidingWindow(self, nums: 'list[int]', k: 'int') -> 'list[int]':
        if len(nums) == 0:
            return []

        queue = []

        for i in range(k):
            while queue != [] and nums[i] > queue[-1]:
                queue.pop()

            queue.append(nums[i])

        result = [queue[0]]

        for i in range(k, len(nums)):
            if nums[i - k] == queue[0]:
                queue.pop(0)
            while queue != [] and nums[i] > queue[-1]:
                queue.pop()
            queue.append(nums[i])
            result.append(queue[0])

        return result
```

