# 【LeetCode with Python】 94. Binary Tree Inorder Traversal
tags: Medium Problems, Tree, Hash Table, Stack

## 题目
原题页面：<https://leetcode.com/problems/binary-tree-inorder-traversal/><br/>
本文地址：<<leetcode-with-python-domain>/binary-tree-inorder-traversal/><br/>
题目类型：Tree, Hash Table, Stack<br/>
难度评价：Medium<br/>
类似题目：[(M) Validate Binary Search Tree](/validate-binary-search-tree/), [(M) Binary Tree Preorder Traversal](/binary-tree-preorder-traversal/), [(H) Binary Tree Postorder Traversal](/binary-tree-postorder-traversal/), [(M) Binary Search Tree Iterator](/binary-search-tree-iterator/), [(M) Kth Smallest Element in a BST](/kth-smallest-element-in-a-bst/), [(H) Closest Binary Search Tree Value II](/closest-binary-search-tree-value-ii/), [(M) Inorder Successor in BST](/inorder-successor-in-bst/)<br/>

> Given a binary tree, return the *inorder* traversal of its nodes' values.<br/>
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
> return `[1,3,2]`.<br/>
><br/>
> **Note:** Recursive solution is trivial, could you do it iteratively?<br/>
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
非递归中序遍历二叉树，每一个计算机和软件专业的朋友大学上数据结构时都会遇到的题之一。总结成一句话就是：有左节点时将左节点压栈，无左节点时出栈一个元素（栈如果是空的则遍历结束），输出该元素，然后如果该元素有右节点则将cur指针跳到该右节点。<br/>
关键在于还是要理解计算机递归的实现原理，然后用程序去加以模拟和实现。例如这题，就可以参考中序遍历二叉树的递归版本，在脑海中模拟一下整个递归过程，即子调用的进入和退出的顺序，就能知道应该用一个栈去模拟这个过程，并且何时入栈和何时出栈。<br/>

---
## 代码
``` python
class Solution:

    # @param root, a tree node
    # @return a list of integers
    def inorderTraversal(self, root):

        if None == root:
            return [ ]

        list = [ ]
        stack = [ ]
        cur = root
        stack.append(cur)

        while True:
            if None != cur and None != cur.left:
                stack.append(cur.left)
                cur = cur.left
                continue
            if len(stack) >= 1:
                cur = stack.pop()
                list.append(cur.val)
                cur = cur.right
            else:
                break
            if None != cur:
                stack.append(cur)

        return list
```
