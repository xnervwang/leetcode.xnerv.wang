# 【LeetCode with Python】 96. Unique Binary Search Trees
tags: Medium Problems, Tree, Dynamic Programming

## 题目
原题页面：<https://leetcode.com/problems/unique-binary-search-trees/><br/>
本文地址：<<leetcode-with-python-domain>/unique-binary-search-trees/><br/>
题目类型：Tree, Dynamic Programming<br/>
难度评价：Medium<br/>
类似题目：[(M) Unique Binary Search Trees II](/unique-binary-search-trees-ii/)<br/>

> Given *n*, how many structurally unique **BST's** (binary search trees) that store values 1...*n*?<br/>
><br/>
> For example,<br/>
> Given *n* = 3, there are a total of 5 unique BST's.<br/>
><br/>
> ```
>    1         3     3      2      1
>     \       /     /      / \      \
>      3     2     1      1   3      2
>     /     /       \                 \
>    2     1         2                 3
> ```

<!-- more -->

---
## 分析
给点节点数，求出能构造出符合二叉搜索树定义的二叉树数量。<br/>
搜索算法。用递归来构建搜索，每次递归时，假设当前子树可分配节点数为n，那就列举每一种分配方案（子树根节点占用一个，第一种方案是左子树分配0个节点，右子树分配n-1个结点；第二种方案左子树分配1个节点，右子树分配n-2个节点；……；最后左子树分配n-1个节点，右子树分配0个节点）并继续子递归。最后累加各个分配方案可以得到的二叉树数量，作为本次递归结果返回。<br/>
空间复杂度与时间复杂度待分析。<br/>
搜索算法一般都可以通过动态规划DP来避免重复的子问题求解，以后有时间了会用DP重新做一次本题。<br/>

---
## 代码
``` python
class Solution:

    def doNumTrees(self, n):
        if n <= 1:
            return 1
        total = 0
        for i in range(0, n):
            left = i
            right = n - left - 1   # 1 as the sub-root node
            total += (self.doNumTrees(left) * self.doNumTrees(right))
        return total

    # @return an integer
    def numTrees(self, n):
        if 0 == n:
            return 0
        return self.doNumTrees(n)
```
