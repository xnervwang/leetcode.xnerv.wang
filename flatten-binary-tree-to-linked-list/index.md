# 【LeetCode with Python】 114. Flatten Binary Tree to Linked List
tags: Medium Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/flatten-binary-tree-to-linked-list/><br/>
本文地址：<http://leetcode.xnerv.wang/flatten-binary-tree-to-linked-list/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Medium<br/>

> Given a binary tree, flatten it to a linked list in-place.<br/>
><br/>
> For example,<br/>
> Given<br/>
> ```
         1
        / \
       2   5
      / \   \
     3   4   6
> ```
><br/>
> The flattened tree should look like:<br/>
> ```
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
> ```
><br/>
> **Hints:**<br/>
> If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.<br/>

<!-- more -->

---
## 分析
题目的算法本身并不难理解，按照先序遍历的节点顺序将一棵二叉树拉平为一个“链表”。因此后序遍历二叉树，先将左子树“拉平”，再将右子树“拉平”，然后如果左子树不是None，就将已经拉平为“链表”的左子树，嵌入到当前节点与直接右孩子节点（可能右孩子是None）之间。关键在于一些分支上要判断是否不为None，很容易出错。<br/>

---
## 代码
``` python
class Solution:
    # @param root, a tree node
    # @return nothing, do it in place
    def flatten(self, root):
        if None == root:
            return
        if None != root.left:
            self.flatten(root.left)
        if None != root.right:
            self.flatten(root.right)
        left = root.left
        right = root.left
        while None != right and None != right.right:
            right = right.right

        if None != right:
            right.right = root.right
        if None != left:     ###
            root.right = left
        root.left = None
```
