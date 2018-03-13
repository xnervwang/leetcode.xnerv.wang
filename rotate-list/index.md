# 【LeetCode with Python】 61. Rotate List
tags: Medium Problems, Linked List, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/rotate-list/><br/>
本文地址：<<leetcode-with-python-domain>/rotate-list/><br/>
题目类型：Linked List, Two Pointers<br/>
难度评价：Medium<br/>
类似题目：[(E) Rotate Array](/rotate-array/)<br/>

> Given a list, rotate the list to the right by *k* places, where *k* is non-negative.<br/>
><br/>
> For example:<br/>
> Given `1->2->3->4->5->NULL` and *k* = `2`,<br/>
> return `4->5->1->2->3->NULL`.<br/>

<!-- more -->

---
## 分析
这类链表倒置，或链表局部倒置的题目，都是大学数据结构课程的日常题目。一般要注意三点：<br/>
1. 在必要的head/tail处设置指针，便于操作；<br/>
2. 注意当节点数n为0、1、2等时的特殊情况下的处理，记得检查指针是否为None；<br/>
3. 有时候head或tail需要特殊处理，此时可以通过增加一个new_head或new_tail，使得head或tail可以被当成普通节点来处理。<br/>

---
## 代码
``` python
class Solution:
    # @param head, a ListNode
    # @param k, an integer
    # @return a ListNode
    def rotateRight(self, head, k):
        if None == head or None == head.next:
            return head
        cur_head = head
        cur = head
        while k > 0:
            cur = cur.next
            if None == cur:
                return head
            k -= 1
        cur_tail = cur
        cur_head = cur.next
        if None == cur_head:
            return head
        cur = cur_head
        while None != cur.next:
            cur = cur.next
        cur.next = head
        cur_tail.next = None
        return cur_head
```
