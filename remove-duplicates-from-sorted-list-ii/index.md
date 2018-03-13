# 【LeetCode with Python】 82. Remove Duplicates from Sorted List II
tags: Medium Problems, Linked List

## 题目
原题页面：<https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/><br/>
本文地址：<<leetcode-with-python-domain>/remove-duplicates-from-sorted-list-ii/><br/>
题目类型：Linked List<br/>
难度评价：Medium<br/>

> Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only *distinct* numbers from the original list.<br/>
><br/>
> For example,<br/>
> Given `1->2->3->3->4->4->5`, return `1->2->5`.<br/>
> Given `1->1->1->2->3`, return `2->3`.<br/>

<!-- more -->

---
## 分析
和Remove Duplicates from Sorted List差不多的题目，区别是对于重复的元素不是去重，而是完全地删除重复出现过的元素。<br/>

---
## 代码
``` python
class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def deleteDuplicates(self, head):
        if None == head or None == head.next:
            return head

        new_head = ListNode(-1)
        new_head.next = head
        parent = new_head
        cur = head
        while None != cur and None != cur.next:   ### check cur.next None
            if cur.val == cur.next.val:
                val = cur.val
                while None != cur and val == cur.val: ### check cur None
                    cur = cur.next
                parent.next = cur
            else:
                cur = cur.next
                parent = parent.next

        return new_head.next
```
