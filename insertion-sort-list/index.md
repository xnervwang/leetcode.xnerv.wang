# 【LeetCode with Python】 147. Insertion Sort List
tags: Medium Problems, Linked List, Sort

## 题目
原题页面：<https://leetcode.com/problems/insertion-sort-list/><br/>
本文地址：<<leetcode-with-python-domain>/insertion-sort-list/><br/>
题目类型：Linked List, Sort<br/>
难度评价：Medium<br/>
类似题目：[(M) Sort List](/sort-list/)<br/>

> Sort a linked list using insertion sort.<br/>

<!-- more -->

---
## 分析
链表的插入排序。先是看到网上有人用C++写的解法，生成一个新的链表，每次都将下一个结点插入到这个新链表中，于是用Python仿写之，然超时。后来改成不再生成新链表，而是直接在原链表上原地排序，并且加入了一个判断条件，避免当需要排序的链表已经有序时再做过多无用功（因为前一次超时的原因就是判题系统给了一个超长的已有序链表-_-）。<br/>

---
## 代码
``` python
class Solution:

    # @param head, a ListNode
    # @return a ListNode
    def insertionSortList(self, head):
        if None == head or None == head.next:
            return head

        new_head = ListNode(0)
        new_head.next = head

        last = new_head.next
        cur = new_head.next.next
        while None != cur:
            if cur.val >= last.val:
                last = cur
                cur = cur.next
                continue
            ins = new_head
            while None != ins.next and ins.next.val <= cur.val: # stable sort
                ins = ins.next
            last.next, cur.next, ins.next, cur = cur.next, ins.next, cur, cur.next

        return new_head.next
```
