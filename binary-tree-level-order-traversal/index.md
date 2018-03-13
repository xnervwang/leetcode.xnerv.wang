# 【LeetCode with Python】 102. Binary Tree Level Order Traversal
tags: Easy Problems, Tree, Breadth-first Search

## 题目
原题页面：<https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/><br/>
本文地址：<http://leetcode.xnerv.wang/binary-tree-level-order-traversal/><br/>
题目类型：Tree, Breadth-first Search<br/>
难度评价：Easy<br/>
类似题目：[(M) Binary Tree Zigzag Level Order Traversal](/binary-tree-level-order-traversal/), [(E) Binary Tree Level Order Traversal II](/binary-tree-level-order-traversal-ii/), [(E) Minimum Depth of Binary Tree](/minimum-depth-of-binary-tree/)<br/>

> Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).<br/>
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
> return its level order traversal as:<br/>
><br/>
> ```
[
  [3],
  [9,20],
  [15,7]
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
二叉树的层次遍历应用在LeetCode中出现了好几次。一般而言二叉树层次遍历是用队列，但是由于本题要区分出每一层，因此用两个数组分别模拟队列。<br/>

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
```
