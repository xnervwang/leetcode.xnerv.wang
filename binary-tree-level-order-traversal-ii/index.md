# 【LeetCode with Python】 107. Binary Tree Level Order Traversal II
tags: Easy Problems, Tree, Breadth-first Search

## 题目
原题页面：<https://leetcode.com/problems/binary-tree-level-order-traversal-ii/><br/>
本文地址：<<leetcode-with-python-domain>/binary-tree-level-order-traversal-ii/><br/>
题目类型：Tree, Breadth-first Search<br/>
难度评价：Easy<br/>
类似题目：[(E) Binary Tree Level Order Traversal](/binary-tree-level-order-traversal/)<br/>

> Given a binary tree, return the *bottom-up level order* traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).<br/>
><br/>
> For example:<br/>
> Given binary tree `{3,9,20,#,#,15,7}`,
><br/>
> ```
    3
   / \
  9  20
    /  \
   15   7
> ```
><br/>
> return its bottom-up level order traversal as:<br/>
><br/>
> ```
[
  [15,7],
  [9,20],
  [3]
]
> ```
><br/>
> confused what `"{1,#,2,3}"` means?
><br/>
> **OJ's Binary Tree Serialization:**<br/>
><br/>
> The serialization of a binary tree follows a level order traversal, where '#' signifies a path terminator where no node exists below.
><br/>
> Here's an example:<br/>
><br/>
> ```
   1
  / \
 2   3
    /
   4
    \
     5
> ```
><br/>
> The above binary tree is serialized as `"{1,2,3,#,#,4,#,#,5}"`.

<!-- more -->

---
## 分析
不知道出题意图是不是希望用递归，从叶子节点到根结点，将每一个节点加入到结果二维数组的相应层次中？<br/>
不过我这里就追求简单，直接将Binary Tree Level Order Traversal的结果数组reverse一下。。。<br/>

---
## 代码
``` python
class Solution:

    # @param root, a tree node
    # @return a list of lists of integers
    def levelOrder(self, root):
        if None == root:
            return [ ]
        results = [ [root.val] ]
        reflist1 = [root]
        while True:
            reflist2 = [ ]
            result = [ ]
            for i in range(0, len(reflist1)):
                cur = reflist1[i]
                if None != cur.left:
                    reflist2.append(cur.left)
                    result.append(cur.left.val)
                if None != cur.right:
                    reflist2.append(cur.right)
                    result.append(cur.right.val)
            if 0 == len(reflist2):
                break
            results.append(result)
            reflist1 = reflist2
        return results

    def levelOrderBottom(self, root):
        results = self.levelOrder(root)
        results.reverse()
        return results
```
