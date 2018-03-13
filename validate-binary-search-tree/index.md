# 【LeetCode with Python】 98. Validate Binary Search Tree
tags: Medium Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/validate-binary-search-tree/><br/>
本文地址：<http://leetcode.xnerv.wang/validate-binary-search-tree/><br/>
题目类型：Medium<br/>
难度评价：Tree, Depth-first Search<br/>
类似题目：[(M) Binary Tree Inorder Traversal](/binary-tree-inorder-traversal/)<br/>

> Given a binary tree, determine if it is a valid binary search tree (BST).<br/>
><br/>
> Assume a BST is defined as follows:<br/>
><br/>
> * The left subtree of a node contains only nodes with keys **less than** the node's key.<br/>
> * The right subtree of a node contains only nodes with keys **greater than** the node's key.<br/>
> * Both the left and right subtrees must also be binary search trees.<br/>
><br/>
> confused what `"{1,#,2,3}"` means?
><br/>
> **OJ's Binary Tree Serialization:**<br/>
><br/>
> The serialization of a binary tree follows a level order traversal, where '#' signifies a path terminator where no node exists below.
><br/>
> Here's an example:<br/>
><br/>
>        1<br/>
>       / \<br/>
>      2   3<br/>
>         /<br/>
>        4<br/>
>         \<br/>
>          5<br/>
><br/>
> The above binary tree is serialized as `"{1,2,3,#,#,4,#,#,5}"`.

<!-- more -->

---
## 分析
检查一颗二叉树是不是有效的二叉搜索树BST。注意BST的定义，不仅仅左孩子结点的值比当前结点小，左子树上所有结点的值都要比当前结点小（BST跟heap是不同，heap只要求每个节点的直接左节点比直接右节点小即可）。右子树上所有结点的值则都要比当前结点大。使用递归检查每一棵子树是不是BST，然后回溯的时候将检查结果，以及当前子树的最大和最小结点值返回给上一层递归。注意Python的return是可以返回一个元组的，相当于可以同时return多个变量，非常方便。<br/>

---
## 代码
``` python
class Solution:

    def recurIsValidBST(self, root):
        if None == root:
            return True, None, None
        elif None == root.left and None == root.right:
            return True, root.val, root.val
        else:
            left_bool, left_min, left_max = self.recurIsValidBST(root.left)
            right_bool, right_min, right_max = self.recurIsValidBST(root.right)
            cur_bool = left_bool and right_bool and (None == left_max or root.val > left_max) and (None == right_min or root.val < right_min)
            cur_max = max(root.val, left_max, right_max)
            cur_min = min(root.val, left_min, right_min)
            return cur_bool, cur_min, cur_max

    # @param root, a tree node
    # @return a boolean
    def isValidBST(self, root):
        return self.recurIsValidBST(root)[0]
```
