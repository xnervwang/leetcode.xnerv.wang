# 【LeetCode with Python】 146. LRU Cache
tags: Hard Problems, Design

## 题目
原题页面：<https://leetcode.com/problems/lru-cache/><br/>
本文地址：<<leetcode-with-python-domain>/lru-cache/><br/>
题目类型：Design<br/>
难度评价：Hard<br/>

> Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: `get` and `set`.<br/>
><br/>
> `get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.<br/>
> `set(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.<br/>

<!-- more -->

---
## 分析
实现一个LRU缓存。最近最少使用LRU表的定义就不多说了，需要实现的get方法是根据key取value的，因此显然需要一个map，在Python里叫关联数组的帮助。虽然在leetcode中这道题被标为Hard级别，但其实这只是一道工程性质的题目。<br/>
另外貌似这道题目的test cases里没有capacity=0的情况？这还是leetcode一贯的作风么？<br/>

---
## 代码
``` python
class LRUCache:

    class LRUNode:
        def __init__(self, key, value):
            self.prev = None
            self.next = None
            self.key = key
            self.value = value

    # @param capacity, an integer
    def __init__(self, capacity):
        self.map = { }
        self.list_head = LRUCache.LRUNode(-1, -1)
        self.list_tail = LRUCache.LRUNode(-1, -1)
        self.list_head.next = self.list_tail
        self.list_tail.prev = self.list_head
        self.capacity = capacity

    def remove_node(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev

    def append_node(self, new_node):
        last_node = self.list_tail.prev
        last_node.next = new_node
        new_node.prev = last_node
        new_node.next = self.list_tail
        self.list_tail.prev = new_node

    # @return an integer
    def get(self, key):
        if self.map.has_key(key):
            cur = self.map.get(key)
            self.remove_node(cur)
            self.append_node(cur)
            return cur.value
        else:
            return -1

    # @param key, an integer
    # @param value, an integer
    # @return nothing
    def set(self, key, value):
        if self.capacity <= 0:
            return
        elif self.map.has_key(key):
            old_node = self.map.get(key)
            self.remove_node(old_node)
            old_node.value = value
            self.append_node(old_node)
        else:
            if len(self.map) >= self.capacity:
                del_node = self.list_head.next
                self.remove_node(del_node)
                del self.map[del_node.key]
            new_node = LRUCache.LRUNode(key, value)
            self.append_node(new_node)
            self.map[key] = new_node
```
