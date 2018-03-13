# 【LeetCode with Python】 104. Maximum Depth of Binary Tree
tags: Easy Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/maximum-depth-of-binary-tree/><br/>
本文地址：<http://leetcode.xnerv.wang/maximum-depth-of-binary-tree/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Easy<br/>
类似题目：[(E) Balanced Binary Tree](/balanced-binary-tree/), [(E) Minimum Depth of Binary Tree](/minimum-depth-of-binary-tree/)<br/>

> Given a binary tree, find its maximum depth.<br/>
><br/>
> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.<br/>

<!-- more -->

---
## 分析
计算二叉树的最大深度，正规的递归回溯解法。<br/>

---
## 代码
``` python
class Solution:

    def recurMaxDepth(self, root, depth):
        if None == root:
            return 0
        elif None == root.left and None == root.right:
            return 1

        left_depth = (self.recurMaxDepth(root.left, depth) if None != root.left else 0)
        right_depth = (self.recurMaxDepth(root.right, depth) if None != root.right else 0)

        # warn: a node just have a child, a node have two child, their height calculation method are different.
        if left_depth > 0 and right_depth > 0:
            return max(left_depth, right_depth) + 1;
        elif left_depth > 0:
            return left_depth + 1
        else:       # right_depth > 0, or (left_depth == 0 and right_depth == 0)
            return right_depth + 1

    # @param root, a tree node
    # @return an integer
    def maxDepth(self, root):
        return self.recurMaxDepth(root, 0)
```
