# 【LeetCode with Python】 92. Reverse Linked List II
tags: Medium Problems, Linked List

## 题目
原题页面：<https://leetcode.com/problems/reverse-linked-list-ii/><br/>
本文地址：<http://leetcode.xnerv.wang/reverse-linked-list-ii/><br/>
题目类型：Linked List<br/>
难度评价：Medium<br/>
类似题目：[(E) Reverse Linked List](/reverse-linked-list/)<br/>

> Reverse a linked list from position *m* to *n*. Do it in-place and in one-pass.<br/>
><br/>
> For example:<br/>
> Given `1->2->3->4->5->NULL`, *m* = 2 and *n* = 4,<br/>
><br/>
> return `1->4->3->2->5->NULL`.<br/>
><br/>
> **Note:**<br/>
> Given *m*, *n* satisfy the following condition:<br/>
> 1 ≤ *m* ≤ *n* ≤ length of list.<br/>

<!-- more -->

---
## 分析
反转链表中的一部分。貌似写出来的代码有点长，也许可以优化。<br/>

---
## 代码
``` python
class Solution:

    # @param head, a ListNode
    # @param m, an integer
    # @param n, an integer
    # @return a ListNode
    def reverseBetween(self, head, m, n):
        if m == n:
            return head

        m_is_head = True if 1 == m else False

        if False == m_is_head:
            m_pre_node = head
            for i in range(0, m - 1 - 1):
                m_pre_node = m_pre_node.next
            m_node = m_pre_node.next
        else:
            m_node = head

        n_node = m_node
        for i in range(0, n - m):
            n_node = n_node.next

        n_next_node = n_node.next
        if False == m_is_head:
            m_pre_node.next = n_node

        p1_node = m_node
        p2_node = p1_node.next
        p3_node = p2_node.next
        while n_node != p1_node:
            p2_node.next = p1_node
            p1_node = p2_node
            p2_node = p3_node
            if None == p2_node:
                break
            p3_node = p3_node.next

        m_node.next = n_next_node

        return n_node if m_is_head else head
```
