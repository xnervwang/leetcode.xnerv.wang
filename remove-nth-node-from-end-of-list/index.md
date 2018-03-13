# 【LeetCode with Python】 19. Remove Nth Node From End of List
tags: Easy Problems, Linked List, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/remove-nth-node-from-end-of-list/><br/>
本文地址：<http://leetcode.xnerv.wang/remove-nth-node-from-end-of-list/><br/>
题目类型：Linked List, Two Pointers<br/>
难度评价：Easy<br/>

> Given a linked list, remove the *n*<sup>th</sup> node from the end of list and return its head.<br/>
><br/>
> For example,<br/>
><br/>
>> Given linked list: **1->2->3->4->5**, and ***n* = 2**.<br/>
>><br/>
>> After removing the second node from the end, the linked list becomes **1->2->3->5**.<br/>
><br/>
> **Note:**<br/>
> Given *n* will always be valid.<br/>
> Try to do this in one pass.<br/>

<!-- more -->

---
## 分析
常见的快慢指针题目。快指针领先慢指针n步，这样当快指针到达尾部时，慢指针正好指向需要删除的节点的父结点。<br/>
注意由于要删除的结点可能刚好是head节点，这种情况与其特殊处理，不如加一个“伪head”，这也是类似的链表类题目的通用做法。<br/>

---
## 代码
``` python
class Solution:
    # @return a ListNode
    def removeNthFromEnd(self, head, n):
        if None == head:
            return head
        if None == head.next:
            return None
        new_head = ListNode(-1)
        new_head.next = head
        fast = new_head
        for i in range(0, n):
            if None != fast.next:
                fast = fast.next
            else:
                return head
        slow = new_head
        while None != fast.next:
            fast = fast.next
            slow = slow.next
        slow.next = slow.next.next
        return new_head.next
```
