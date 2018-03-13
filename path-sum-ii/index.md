# 【LeetCode with Python】 113. Path Sum II
tags: Medium Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/path-sum-ii/><br/>
本文地址：<<leetcode-with-python-domain>/path-sum-ii/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Medium<br/>
类似题目：[(E) Path Sum](/path-sum/), [(E) Binary Tree Paths](/binary-tree-paths/)<br/>

> Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.<br/>
><br/>
> For example:<br/>
> Given the below binary tree and `sum = 22`,<br/>
><br/>
>                   5<br/>
>                  / \<br/>
>                 4   8<br/>
>                /   / \<br/>
>               11  13  4<br/>
>              /  \    / \<br/>
>             7    2  5   1<br/>
><br/>
> return<br/>
><br/>
>     [<br/>
>        [5,4,11,2],<br/>
>        [5,8,4,5]<br/>
>     ]<br/>

<!-- more -->

---
## 分析
和Path Sum差不多，不过要记录一下所有可行解。<br/>

---
## 代码
``` python
class Solution:

    def __init__(self):
        self.paths = [ ]

    def doPathSum(self, root, total, sum, path):
        if None == root.left and None == root.right:
            path.append(root.val)
            result = (sum == (total + root.val))
            if True == result:
                self.paths.append(path)

        left= False
        right = False
        if None != root.left:
            new_path = path[:]
            new_path.append(root.val)
            left = self.doPathSum(root.left, total + root.val, sum, new_path)
        if None != root.right:
            new_path = path[:]
            new_path.append(root.val)
            right = self.doPathSum(root.right, total + root.val, sum, new_path)
        return left or right

    # @param root, a tree node
    # @param sum, an integer
    # @return a list of lists of integers
    def pathSum(self, root, sum):
        if None == root:
            return [ ] ###
        result = self.doPathSum(root, 0, sum, [ ])
        return self.paths
```
