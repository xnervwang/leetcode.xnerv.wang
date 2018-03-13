# 【LeetCode with Python】 124. Binary Tree Maximum Path Sum
tags: Hard Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/binary-tree-maximum-path-sum/><br/>
本文地址：<http://leetcode.xnerv.wang/binary-tree-maximum-path-sum/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Hard<br/>
类似题目：[(M) Path Sum](/path-sum/), [(M) Sum Root to Leaf Numbers](sum-root-to-leaf-numbers)<br/>

> Given a binary tree, find the maximum path sum.<br/>
><br/>
> For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path does not need to go through the root.<br/>
><br/>
> For example:<br/>
> Given the below binary tree,<br/>
><br/>
>            1<br/>
>           / \<br/>
>          2   3<br/>
><br/>
> Return `6`.<br/>

<!-- more -->

---
## 分析
本是比较简单的一道二叉树递归算法题目，也花了一些时间。主要还是在题意的理解中，本题要求的“最大路径和”，不一定经过了root，起点和终点可以是同一个点（即整个路径只有一个点）。<br/>
注意用一个类成员变量max来记录搜索过程中出现过的最大路径和，最后需要返回的就是这个max值。<br/>
此外还有一点容易搞错，当一棵子树计算完退栈时，向上一层返回的应该是该子树左路径、右路径中的最大值，而不是该子树中的“最大路径和”，因为从父节点搜索进入该子树时，只能选择其左分支或者右分治进入。<br/>
最后需要注意的一点是，这道题目并没有说节点的值是正数或者自然数，考虑到leetcode一贯的尿性，最好认为负数也是会出现的。<br/>

---
## 代码
``` python
class Solution:
    def __init__(self):
        self.max = None

    def doMaxPathSum(self, root):
        if None == root:
            return 0
        left_sum = self.doMaxPathSum(root.left)
        right_sum = self.doMaxPathSum(root.right)
        max_left_sum = max(left_sum, 0)
        max_right_sum = max(right_sum, 0)
        cur_max = max_left_sum + max_right_sum + root.val
        if None == self.max or cur_max > self.max:
            self.max = cur_max
        return max(max_left_sum + root.val, max_right_sum + root.val)

    # @param root, a tree node
    # @return an integer
    def maxPathSum(self, root):
        self.doMaxPathSum(root)
        return self.max
```
