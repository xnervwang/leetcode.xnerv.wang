# 【LeetCode with Python】 86. Partition List
tags: Medium Problems, Linked List, Two Pointers

## 题目
原题页面：<https://oj.leetcode.com/problems/partition-list/><br/>
本文地址：<<leetcode-with-python-domain>/partition-list/><br/>
题目类型：Linked List, Two Pointers<br/>
难度评价：Medium<br/>

> Given a linked list and a value *x*, partition it such that all nodes less than *x* come before nodes greater than or equal to *x*.<br/>
><br/>
> You should preserve the original relative order of the nodes in each of the two partitions.<br/>
><br/>
> For example,<br/>
> Given `1->4->3->2->5->2` and *x* = 3,<br/>
> return `1->2->2->4->3->5`.<br/>

<!-- more -->

---
## 分析

---
## 代码
``` python
class Solution:
    # @param head, a ListNode
    # @param x, an integer
    # @return a ListNode
    def partition(self, head, x):
        if None == head or None == head.next:
            return head
        new_head = ListNode(-1)
        new_head.next = head
        tail = head
        while None != tail.next:
            tail = tail.next
        cur = head
        parent = new_head
        l_pos = new_head

        while tail != parent and None != cur:
            if cur.val >= x:
                break
            parent = parent.next
            cur =  cur.next
            l_pos = l_pos.next
        parent =  parent.next
        if None != cur:
            cur = cur.next
        #l_pos = l_pos.next

        while tail != parent and None != cur:
            if cur.val < x:
                parent.next = cur.next
                cur.next = l_pos.next
                l_pos.next = cur
                l_pos = l_pos.next
                cur = parent.next
            else:
                parent = parent.next
                cur =  cur.next
        return new_head.next
```
