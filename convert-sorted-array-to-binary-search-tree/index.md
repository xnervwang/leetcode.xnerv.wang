# 【LeetCode with Python】 108. Convert Sorted Array to Binary Search Tree
tags: Medium Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/><br/>
本文地址：<http://leetcode.xnerv.wang/convert-sorted-array-to-binary-search-tree/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Medium<br/>
类似题目：[(M) Convert Sorted List to Binary Search Tree](/convert-sorted-list-to-binary-search-tree/)<br/>

> Given an array where elements are sorted in ascending order, convert it to a height balanced BST.<br/>

<!-- more -->

---
## 分析
用递归的方法，每次选择当前子序列的中点作为子树的root，然后再递归对左边子序列和右边子序列进行处理。<br/>
原题中标注为深度搜索DFS。这里是构建二叉树，构建的顺序类似于二叉树的先序遍历。由于树是一种特殊的图，因此二叉树的先序遍历其实就是图的DFS，而层次遍历就是图的BFS。<br/>

---
## 代码
``` python
class Solution:

    def doSortedArrayToBST(self, num, start, end):
        if start > end:
            return None
        mid = start + (end - start) / 2
        root = TreeNode(num[mid])
        root.left = self.doSortedArrayToBST(num, start, mid - 1)
        root.right = self.doSortedArrayToBST(num, mid + 1, end)
        return root

    # @param num, a list of integers
    # @return a tree node
    def sortedArrayToBST(self, num):
        len_num = len(num)
        if 0 == len_num:
            return None
        return self.doSortedArrayToBST(num, 0, len_num - 1)
```
