# 【LeetCode with Python】 144. Binary Tree Preorder Traversal
tags: Medium Problems, Tree, Stack

## 题目
原题页面：<https://leetcode.com/problems/binary-tree-preorder-traversal/><br/>
本文地址：<http://leetcode.xnerv.wang/binary-tree-preorder-traversal/><br/>
题目类型：Tree, Stack<br/>
难度评价：Medium<br/>
类似题目：[(M) Binary Tree Inorder Traversal](/binary-tree-inorder-traversal/), [(M) Verify Preorder Sequence in Binary Search Tree](/verify-preorder-sequence-in-binary-search-tree/)<br/>

> Given a binary tree, return the *preorder* traversal of its nodes' values.<br/>
><br/>
> For example:<br/>
> Given binary tree `{1,#,2,3}`,
><br/>
>        1<br/>
>         \<br/>
>          2<br/>
>         /<br/>
>        3<br/>
><br/>
> return `[1,2,3]`.<br/>
><br/>
> **Note:** Recursive solution is trivial, could you do it iteratively?<br/>

<!-- more -->

---
## 分析
非递归前序遍历二叉树。这里是用栈，先右孩子入栈，再左孩子入栈。隐约还记得如果是层次遍历，即需要用队列了。二叉树的非递归遍历中，记得后序遍历是最复杂的，需要用两个栈，以后再复习一下后序遍历。<br/>

---
## 代码
``` python
class Solution:

    # @param root, a tree node
    # @return a list of integers
    def preorderTraversal(self, root):

        if None == root:
            return [ ]

        list = [ ]
        stack = [ ]
        cur = root

        while True:
            list.append(cur.val)
            if None != cur.right:
                stack.append(cur.right)
            if None != cur.left:
                stack.append(cur.left)
            if len(stack) >= 1:
                cur = stack.pop()
            else:
                break

        return list
```
