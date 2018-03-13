# 【LeetCode with Python】 24. Swap Nodes in Pairs
tags: Medium Problems, Linked List

## 题目
原题页面：<https://leetcode.com/problems/swap-nodes-in-pairs/><br/>
本文地址：<<leetcode-with-python-domain>/swap-nodes-in-pairs/><br/>
题目类型：Medium<br/>
难度评价：Linked List<br/>
类似题目：[(H) Reverse Nodes in k-Group](/reverse-nodes-in-k-group/)<br/>

> Given a linked list, swap every two adjacent nodes and return its head.<br/>
><br/>
> For example,<br/>
> Given `1->2->3->4`, you should return the list as `2->1->4->3`.<br/>
><br/>
> Your algorithm should use only constant space. You may **not** modify the values in the list, only nodes itself can be changed.<br/>

<!-- more -->

---
## 分析
交换单链表中每一对相邻的奇偶数下标的元素，注意防止链表长度可能是奇数，即不要忘记检查second_node是否为None。<br/>

---
## 代码
``` python
class Solution:
    # @param a ListNode
    # @return a ListNode
    def swapPairs(self, head):
        if None == head:
            return head
        new_head = ListNode(0)
        new_head.next = head
        last_node = new_head
        while True:
            first_node = last_node.next
            if None == first_node:
                break
            second_node = first_node.next
            if None == second_node:
                break
            last_node.next,  first_node.next, second_node.next, last_node = second_node, second_node.next, first_node, first_node
        return new_head.next
```
