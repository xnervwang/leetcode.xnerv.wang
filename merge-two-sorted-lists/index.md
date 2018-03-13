# 【LeetCode with Python】 21. Merge Two Sorted Lists
tags: Easy Problems, Linked List

## 题目
原题页面：<https://leetcode.com/problems/merge-two-sorted-lists/><br/>
本文地址：<<leetcode-with-python-domain>/merge-two-sorted-lists/><br/>
题目类型：Linked List<br/>
难度评价：Easy<br/>
类似题目：[(H) Merge k Sorted Lists](/merge-k-sorted-lists/), [(E) Merge Sorted Array](/merge-sorted-array/), [(M) Sort List](/sort-list/), [(M) Shortest Word Distance II](/shortest-word-distance-ii/)<br/>

> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.<br/>

<!-- more -->

---
## 分析
合并两个有序链表，大学期间常见的数据结构练习题。用两个指针分别指向两个链表头，然后每次都将两者中最小的那个节点加入到到合并后的链表尾部。注意当其中一个链表的节点全部处理完时，别忘了将另一个链表剩余的节点依次全部加入到合并后的链表尾部。<br/>

---
## 代码
``` python
class Solution:
    # @param two ListNodes
    # @return a ListNode
    def mergeTwoLists(self, l1, l2):
        if None == l1 and None == l2:
            return None
        elif None == l1:
            return l2
        elif None == l2:
            return l1

        new_list = ListNode(0)
        cur = new_list
        node1 = l1
        node2 = l2
        while None != node1 and None != node2:
            if node1.val < node2.val:
                cur.next = node1
                node1 = node1.next
            else:
                cur.next = node2
                node2 = node2.next
            cur = cur.next
        if None != node1:
            cur.next = node1
        else:
            cur.next = node2

        return new_list.next
```
