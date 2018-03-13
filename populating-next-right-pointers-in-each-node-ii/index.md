# 【LeetCode with Python】 117. Populating Next Right Pointers in Each Node II
tags: Hard Problems, Tree, Depth-first Search, todo

## 题目
原题页面：<https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/><br/>
本文地址：<http://leetcode.xnerv.wang/populating-next-right-pointers-in-each-node-ii/><br/>
题目类型：Tree, Depth-first SearchTwo Pointers<br/>
难度评价：Hard<br/>
类似题目：[(M) Populating Next Right Pointers in Each Node](/populating-next-right-pointers-in-each-node/)<br/>

> Follow up for problem "*Populating Next Right Pointers in Each Node*".<br/>
><br/>
> What if the given tree could be any binary tree? Would your previous solution still work?<br/>
><br/>
> **Note:**<br/>
> * You may only use constant extra space.<br/>
><br/>
> For example,<br/>
> Given the following binary tree,<br/>
><br/>
>              1<br/>
>            /  \<br/>
>           2    3<br/>
>          / \    \<br/>
>         4   5    7<br/>
><br/>
> After calling your function, the tree should look like:<br/>
><br/>
>              1 -> NULL<br/>
>            /  \<br/>
>           2 -> 3 -> NULL<br/>
>          / \    \<br/>
>         4-> 5 -> 7 -> NULL<br/>

<!-- more -->

---
## 分析
复用[Populating Next Right Pointers in Each Node](/populating-next-right-pointers-in-each-mode/)的代码直接可以通过。<br/>
（但是本题代码可能不符合题意要求，题目要求消耗常量空间）<br/>

---
## 代码
``` python
# Definition for a  binary tree node
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
        self.next = None

class Solution:
    # @param root, a tree node
    # @return nothing
    def connect(self, root):
        if None == root:
            return [ ]
        reflist1 = [root]
        while True:
            reflist2 = [ ]
            for i in range(0, len(reflist1)):
                cur = reflist1[i]
                if None != cur.left:
                    reflist2.append(cur.left)
                if None != cur.right:
                    reflist2.append(cur.right)
            if 0 == len(reflist2):
                break
            len_l = len(reflist2)
            for i in range(0, len_l - 1):
                reflist2[i].next = reflist2[i + 1]
            reflist2[len_l - 1].next = None
            reflist1 = reflist2
```
