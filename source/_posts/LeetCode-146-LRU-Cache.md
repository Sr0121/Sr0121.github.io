---
title: 'LeetCode:146. LRU Cache'
date: 2019-06-09 11:03:42
categories: LeetCode
tags: 
  - LeetCode
  - C++
---

**题目概述**

Design and implement a data structure for [Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations: `get` and `put`.

`get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a **positive** capacity.

**Follow up:**
Could you do both operations in **O(1)** time complexity?

**Example:**

```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```


<!--more-->

本题本质上就是模拟cache的替换策略。当cache没有满时进行put操作会直接按顺序将cache填充满，如果cache满后进行put操作，将会替代掉最先使用的key的信息。

所以本题就是维护一个数组keys，这个数组的最左边的key为最先使用的key，最右边则为最近使用的key。同时，还需要用一个keyMap来存放所有key对应的value值。我令所有的key最初为-1，在进行put(key, value)操作时：

1. 如果数组keys中存在这个key时，把这个key右边的所有信息左移一格。然后在所有有效信息（非-1信息）的最右边加上这个key，保证数组能够存储keys的使用先后信息
2. 如果keys中不存在这个key，并且keys数组没有满，则在所有有效信息的最右边加上这个key
3. 如果keys中不存在这个key，并且keys数组已满，则将最左边的key删除，把所有的key向左移动一格，最后在最右边加上这个key

在进行get(key)操作时候：

1. 如果keys不存在这个key，则返回-1
2. 如果keys存在这个key，按照put才做中的1来操作keys数组，并且在keyMap中查找对应的值进行返回



**代码实现**

```c++
class LRUCache {
public:
    LRUCache(int capacity) {
        this->keys = (int*)malloc(sizeof(int)*capacity);
        for (int i = 0; i < capacity; i++) {
            this->keys[i] = -1;
        }
        this->capacity = capacity;
    }

    int get(int key) {
        for (int i = 0; i < this->capacity; i++){
            if (this->keys[i] == key){
                this->modify(i, key);
                return this->keyMap[key];
            }
        }
        return -1;
    }

    void put(int key, int value) {
        for (int i = 0; i < this->capacity; i++){
            if (this->keys[i] == key) {
                this->keyMap[key] = value;
                this->modify(i, key);
                return;
            }
            if (this->keys[i] == -1) {
                this->keyMap[key] = value;
                this->keys[i] = key;
                return;
            }
        }
        this->keyMap.erase(this->keys[0]);
        this->keyMap[key] = value;
        this->add(key);
    }

private:
    int *keys;
    int capacity;
    map<int, int> keyMap;

    void modify(int index, int key){
        int i;
        for(i = index; i < this->capacity-1; i++){
            this->keys[i] = this->keys[i+1];
            if (this->keys[i] == -1) {
                this->keys[i] = key;
                return;
            }
        }
        if (i == capacity-1){
            this->keys[i] = key;
        }
    }

    void add(int key){
        for(int i = 0; i < this->capacity-1; i++){
            this->keys[i] = this->keys[i+1];
        }
        this->keys[this->capacity-1] = key;
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

