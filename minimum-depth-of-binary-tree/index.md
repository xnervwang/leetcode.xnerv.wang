# 【LeetCode with Python】 111. Minimum Depth of Binary Tree
tags: Easy Problems, Tree, Depth-first Search, Breadth-first Search

## 题目
原题页面：<https://leetcode.com/problems/minimum-depth-of-binary-tree/><br/>
本文地址：<http://leetcode.xnerv.wang/minimum-depth-of-binary-tree/><br/>
题目类型：Tree, Depth-first Search, Breadth-first Search<br/>
难度评价：Easy<br/>
类似题目：[(E) Binary Tree Level Order Traversal](/binary-tree-level-order-traversal/), [(E) Meeting Rooms](/meeting-rooms/), [(E) Maximum Depth of Binary Tree](/maximum-depth-of-binary-tree/)<br/>

> Given a binary tree, find its minimum depth.<br/>
><br/>
> The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.<br/>

<!-- more -->

---
## 分析
计算二叉树的最小深度。好像还有另外一道题是计算二叉树的最大深度，其实解法都类似，递归加回溯。<br/>
但是要注意一点的是，如果一个node的左子树高度是2，右子树高度是0，则说明node是没有右节点的，此时node为root的子树的最小高度**应该是2+1=3，而不应该是0+1=2**。<br/>

---
## 代码
``` python
class Solution:

    def recurMinDepth(self, root, depth):
        if None == root:
            return 0
        elif None == root.left and None == root.right:
            return 1

        left_depth = (self.recurMinDepth(root.left, depth) if None != root.left else 0)
        right_depth = (self.recurMinDepth(root.right, depth) if None != root.right else 0)

        # warn: a node just have a child, a node have two child, their height calculation method are different.
        if left_depth > 0 and right_depth > 0:
            return min(left_depth, right_depth) + 1;
        elif left_depth > 0:
            return left_depth + 1
        else:       # right_depth > 0, or (left_depth == 0 and right_depth == 0)
            return right_depth + 1

    # @param root, a tree node
    # @return an integer
    def minDepth(self, root):
        return self.recurMinDepth(root, 0)
```
