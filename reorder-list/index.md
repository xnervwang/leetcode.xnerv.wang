# 【LeetCode with Python】 143. Reorder List
tags: Medium Problems, Linked List

## 题目
原题页面：<https://leetcode.com/problems/reorder-list/><br/>
本文地址：<http://leetcode.xnerv.wang/reorder-list/><br/>
题目类型：Linked List<br/>
难度评价：Medium<br/>

> Given a singly linked list *L*: *L*<sub>0</sub>→*L*<sub>1</sub>→…→*L*<sub>*n*-1</sub>→*L*<sub>n</sub>,<br/>
> reorder it to: *L*<sub>0</sub>→*L*<sub>*n*</sub>→*L*<sub>1</sub>→*L*<sub>*n*-1</sub>→*L*<sub>2</sub>→*L*<sub>*n*-2</sub>→…<br/>
><br/>
> You must do this in-place without altering the nodes' values.<br/>
><br/>
> For example,<br/>
> Given `{1,2,3,4}`, reorder it to `{1,4,2,3}`.<br/>

<!-- more -->

---
## 分析
将链表倒置过来，然后再和原链表进行穿插。是不是有更好的方法？（等等什么情况，没有拷贝原链表就倒置，原本的链表顺序不就被破坏了么？？？）<br/>

---
## 代码
``` python
class Solution:

    # @param head, a ListNode
    # @return nothing
    def reorderList(self, head):

        if None == head:
            return
        cur = head
        count = 0
        while None != cur:
            cur = cur.next
            count += 1
        if count <= 2:
            return

        half_count = (count - 1) / 2
        cur2 = head
        for i in range(0, half_count):
            cur2= cur2.next
        cur2_next = cur2.next
        cur2.next = None
        cur2 = reverse_list(cur2_next, None, None)

        cur1 = head
        time_count = int(count / 2)
        for i in range(0, time_count):
            cur2_next = cur2.next
            cur2.next = cur1.next
            cur1.next = cur2
            cur1 = cur2.next
            cur2 = cur2_next
```
