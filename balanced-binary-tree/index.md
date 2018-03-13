# 【LeetCode with Python】 110. Balanced Binary Tree
tags: Easy Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/balanced-binary-tree/><br/>
本文地址：<<leetcode-with-python-domain>/balanced-binary-tree/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Easy<br/>
类似题目：[(E) Maximum Depth of Binary Tree](/maximum-depth-of-binary-tree/)<br/>

> Given a binary tree, determine if it is height-balanced.<br/>
><br/>
> For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.<br/>

<!-- more -->

---
## 分析
判断一棵树是否高度平衡，即每个节点的左右子树高度相差不过1，参考BBT二叉平衡树或AVL的定义。还是用常见的二叉树递归回溯解法。<br/>

---
## 代码
``` python
class Solution:
    def checkBBT(self, root):
        if None == root:
            return True, 0
        isLeftBBT, leftDepth = self.checkBBT(root.left)
        isRightBBT, rightDepth = self.checkBBT(root.right)
        isBBT = isLeftBBT and isRightBBT and abs(leftDepth - rightDepth) <= 1
        depth = max(leftDepth, rightDepth) + 1
        return isBBT, depth

    # @param root, a tree node
    # @return a boolean
    def isBalanced(self, root):
        return self.checkBBT(root)[0]
```
