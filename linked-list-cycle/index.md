# 【LeetCode with Python】 141. Linked List Cycle
tags: Medium Problems, Linked List, Two Pointers

## 题目
原题页面：<https://leetcode.com/problems/linked-list-cycle/><br/>
本文地址：<http://leetcode.xnerv.wang/linked-list-cycle/><br/>
题目类型：Linked List, Two Pointers<br/>
难度评价：Medium<br/>
类似题目：[(M) Linked List Cycle II](/linked-list-cycle-ii/)<br/>

> Given a linked list, determine if it has a cycle in it.<br/>
><br/>
> Follow up:<br/>
> Can you solve it without using extra space?<br/>

<!-- more -->

---
## 分析
确定链表是否有环。记得好像是编程之美上的题目？<br/>

用两个指针。一个是快指针，每轮走两步。一个是慢指针，每轮走一步。如果链表有环，则总会有某个时刻，快慢指针会相遇在同一个节点。<br/>

如何证明呢？假设现在两个指针都已经进入了环，快指针每次都比慢指针多走一步。那么当某个时刻，快指针要么在慢指针后面一个节点处，要么在其后面两个节点处。如果是前者，则下一次两者就会相遇。如果是后者，则下一次走动后，快指针将位于慢指针后面一个节点处，则又回到了前者的情形。所以两个指针必然会相遇到环上的某个节点处。<br/>

---
## 代码
``` python
class Solution:
    # @param head, a ListNode
    # @return a boolean
    def hasCycle(self, head):
        if None == head:
            return False
        fast = slow = head
        while True:
            fast = fast.next
            if None == fast:
                return False
            fast = fast.next
            if None == fast:
                return False
            slow = slow.next
            if fast == slow:
                return True
```
