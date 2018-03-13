# 【LeetCode with Python】 100. Same Tree
tags: Easy Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/same-tree/><br/>
本文地址：<<leetcode-with-python-domain>/same-tree/><br/>
题目类型：Easy<br/>
难度评价：Tree, Depth-first Search<br/>

> Given two binary trees, write a function to check if they are equal or not.<br/>
><br/>
> Two binary trees are considered equal if they are structurally identical and the nodes have the same value.<br/>

<!-- more -->

---
## 分析
判断两个二叉树是否相等。常见的二叉树递归回溯算法。<br/>

---
## 代码
``` python
class Solution:

    # @param p, a tree node
    # @param q, a tree node
    # @return a boolean
    def isSameTree(self, p, q):
        if None == p and None == q:
            return True
        elif (None == p and None != q) or (None != p and None == q):
            return False
        else:
            return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```
