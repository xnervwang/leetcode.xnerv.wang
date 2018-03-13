# 【LeetCode with Python】 2. Add Two Numbers
tags: Medium Problems, Linked List, Math

## 题目
原题页面：<https://leetcode.com/problems/add-two-numbers/><br/>
本文地址：<http://leetcode.xnerv.wang/add-two-numbers/><br/>
题目类型：Linked List, Math<br/>
难度评价：Medium<br/>
类似题目：[(M) Multiply Strings](/multiply-strings/), [(E) Add Binary](/add-binary/)<br/>

> You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.<br/>
><br/>
> **Input:** (2 -> 4 -> 3) + (5 -> 6 -> 4)<br/>
> **Output:** 7 -> 0 -> 8<br/>

<!-- more -->

---
## 分析
一开始还想复杂了，以为链表头是最高位，于是还准备通过递归来解决。后来才发现原来原来链表头就是最低位，于是这题目的难度就几乎为0了。注意进位的处理，尤其是最后可能的进位。<br/>

---
## 代码
``` python
class Solution:
    # @return a ListNode
    def addTwoNumbers(self, l1, l2):
        cur1 = l1
        cur2 = l2
        carry = 0
        head = ListNode(-1)
        cur = head
        while None != cur1 and None != cur2:
            plus = cur1.val + cur2.val + carry
            digit = plus % 10
            carry = plus / 10
            cur.next = ListNode(digit)
            cur = cur.next
            cur1 = cur1.next
            cur2 = cur2.next

        if None != cur1:
            while None != cur1:
                plus = cur1.val + carry
                digit = plus % 10
                carry = plus / 10
                cur.next = ListNode(digit)
                cur = cur.next
                cur1 = cur1.next
        elif None != cur2:
            while None != cur2:
                plus = cur2.val + carry
                digit = plus % 10
                carry = plus / 10
                cur.next = ListNode(digit)
                cur = cur.next
                cur2 = cur2.next
        if None == cur1 and None == cur2:    ###must after if and elif
            if 1 == carry:
                cur.next = ListNode(1)

        return head.next
```
