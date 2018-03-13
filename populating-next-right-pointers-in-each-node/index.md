# 【LeetCode with Python】 116. Populating Next Right Pointers in Each Node
tags: Medium Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/populating-next-right-pointers-in-each-node/><br/>
本文地址：<<leetcode-with-python-domain>/populating-next-right-pointers-in-each-node/><br/>
题目类型：Tree, Depth-first SearchTwo Pointers<br/>
难度评价：Medium<br/>
类似题目：[(H) Populating Next Right Pointers in Each II Node](/populating-next-right-pointers-in-each-node-ii/), [(M) Binary Tree Right Side View](/binary-tree-right-side-view/)<br/>

> Given a binary tree<br/>
><br/>
>         struct TreeLinkNode {<br/>
>           TreeLinkNode *left;<br/>
>           TreeLinkNode *right;<br/>
>           TreeLinkNode *next;<br/>
>         }<br/>
><br/>
> Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.<br/>
><br/>
> Initially, all next pointers are set to `NULL`.<br/>
><br/>
> **Note:**<br/>
><br/>
> * You may only use constant extra space.<br/>
> * You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).<br/>
><br/>
> For example,<br/>
> Given the following perfect binary tree,<br/>
><br/>
>              1<br/>
>            /  \<br/>
>           2    3<br/>
>          / \  / \<br/>
>         4  5  6  7<br/>
><br/>
> After calling your function, the tree should look like:<br /><br/>
><br/>
>              1 -> NULL<br/>
>            /  \<br/>
>           2 -> 3 -> NULL<br/>
>          / \  / \<br/>
>         4->5->6->7 -> NULL<br/>

<!-- more -->

---
## 分析
类似于层次遍历的方法，参考[Binary Tree Level Order Traversal](/binary-tree-level-order-traversal/)这道题的代码，其实就是在其基础上加上了对一层结点的next指针的处理逻辑。<br/>
此外，这道题的衍生版本[Populating Next Right Pointers in Each Node II](/populating-next-right-pointers-in-each-node-ii/)与本题的区别是，本题是完全二叉树，而[Populating Next Right Pointers in Each Node II](/populating-next-right-pointers-in-each-node-ii/)却可能是任意结构的二叉树。但本题的代码对于这两道题都可以通过。<br/>
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
