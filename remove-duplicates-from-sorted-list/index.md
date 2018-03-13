# 【LeetCode with Python】 83. Remove Duplicates from Sorted List
tags: Easy Problems, Linked List

## 题目
原题页面：<https://leetcode.com/problems/remove-duplicates-from-sorted-list/><br/>
本文地址：<<leetcode-with-python-domain>/remove-duplicates-from-sorted-list/><br/>
题目类型：Linked List<br/>
难度评价：Easy<br/>

> Given a sorted linked list, delete all duplicates such that each element appear only *once*.<br/>
><br/>
> For example,<br/>
> Given `1->1->2`, return `1->2`.<br/>
> Given `1->1->2->3->3`, return `1->2->3`.<br/>

<!-- more -->

---
## 分析
有序链表的去重，注意及时检查一些引用是否为None。<br/>

---
## 代码
``` python
class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def deleteDuplicates(self, head):
        if None == head or None == head.next:
            return head

        cur = head
        while None != cur:
            if None != cur.next and cur.val == cur.next.val:
                cur.next = cur.next.next
                continue
            else:
                cur = cur.next

        return head
```
