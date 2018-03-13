# 【LeetCode with Python】 148. Sort List
tags: Medium Problems, Linked List, Sort

## 题目
原题页面：<https://leetcode.com/problems/sort-list/><br/>
本文地址：<http://leetcode.xnerv.wang/sort-list/><br/>
题目类型：Linked List, Sort<br/>
难度评价：Medium<br/>
类似题目：[(E) Merge Two Sorted Lists](/merge-two-sorted-lists/), [(M) Sort Colors](/sort-colors/), [(M) Insertion Sort List](/insertion-sort-list/)<br/>

> Sort a linked list in *O*(*n* log *n*) time using constant space complexity.<br/>

<!-- more -->

---
## 分析
链表的快速排序。<br/>

---
## 代码
``` python
class Solution:

    def findMiddle(self, head):
        slow = head
        fast = head.next
        while None != fast and None != fast.next:
            fast = fast.next.next
            slow = slow.next
        return slow

    def mergeList(self, head):
        if None == head.next:
            return head
        mid = self.findMiddle(head)
        right_head = mid.next
        mid.next = None
        left_list = self.mergeList(head)
        right_list = self.mergeList(right_head)
        new_head = ListNode(-1)
        new_tail = new_head
        left_node = left_list
        right_node = right_list
        while None != left_node and None != right_node:
            if left_node.val <= right_node.val:
                new_tail.next = left_node
                left_node = left_node.next
            else:
                new_tail.next = right_node
                right_node = right_node.next
            new_tail = new_tail.next
        new_tail.next = left_node if None != left_node else right_node
        return new_head.next

    # @param head, a ListNode
    # @return a ListNode
    def sortList(self, head):
        if None == head:            # leetcode will input this !
            return None
        return self.mergeList(head)
```
