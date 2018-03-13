# 【LeetCode with Python】 138. Copy List with Random Pointer
tags: Hard Problems, Hash Table, Linked List

## 题目
原题页面：<https://leetcode.com/problems/copy-list-with-random-pointer/><br/>
本文地址：<<leetcode-with-python-domain>/copy-list-with-random-pointer/><br/>
题目类型：Hash Table, Linked List<br/>
难度评价：Hard<br/>
类似题目：[(M) Clone Graph](/clone-graph/)<br/>

> A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.<br/>
><br/>
> Return a deep copy of the list.<br/>

<!-- more -->

---
## 分析

---
## 代码
``` python
# Definition for singly-linked list with a random pointer.
class RandomListNode:
    def __init__(self, x):
        self.label = x
        self.next = None
        self.random = None

class Solution:
    # @param head, a RandomListNode
    # @return a RandomListNode
    def copyRandomList(self, head):
        if None == head:
            return None
        save_list = [ ]
        p1 = head
        while None != p1:
            save_list.append(p1)
            p1 = p1.next
        new_head = RandomListNode(-1)
        new_head.next = head
        first = new_head
        second = head
        copy_head = RandomListNode(-1)
        copy_first = copy_head
        copy_second = None
        while None != first:
            copy_second = RandomListNode(second.label) if None != second else None
            copy_first.next = copy_second
            copy_first = copy_first.next
            first = first.next
            if None != second:
                second = second.next

        p1 = head
        p1_tail = head.next
        p2 = copy_head.next
        while None != p1:
            p1_tail = p1.next
            p1.next = p2
            p2.random = p1
            p1 = p1_tail
            p2 = p2.next
        p2 = copy_head.next
        #p1 = head
        while None != p2:
            p2.random = p2.random.random.next if None != p2.random.random else None
            #p1.next = p1.next.next.random if None != p1.next.next else None   # may broken the previous p1.next, so have to save ori list
            p2 = p2.next
            #p1 = p1.next
        len_save_list = len(save_list)
        for i in range(0, len_save_list - 1):
            save_list[i].next = save_list[i + 1]
        save_list[len_save_list - 1].next = None
        return copy_head.next
```
