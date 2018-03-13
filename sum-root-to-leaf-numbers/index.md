# 【LeetCode with Python】 129. Sum Root to Leaf Numbers
tags: Medium Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/sum-root-to-leaf-numbers/><br/>
本文地址：<http://leetcode.xnerv.wang/sum-root-to-leaf-numbers/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Medium<br/>
类似题目：[(E) Path Sum](/path-sum/), [(H) Binary Tree Maximum Path Sum](/binary-tree-maximum-path-sum/)<br/>

> Given a binary tree containing digits from `0-9` only, each root-to-leaf path could represent a number.<br/>
> An example is the root-to-leaf path `1->2->3` which represents the number `123`.<br/>
><br/>
> Find the total sum of all root-to-leaf numbers.<br/>
><br/>
> For example,<br/>
> ```
    1
   / \
  2   3
> ```
><br/>
> The root-to-leaf path `1->2` represents the number `12`.<br/>
> The root-to-leaf path `1->3` represents the number `13`.<br/>
><br/>
> Return the sum = 12 + 13 = `25`.<br/>

<!-- more -->

---
## 分析
从根节点到叶子节点的路径代表一个数值，找出所有的这些数值然后累加得到一个和。<br/>
搜索算法可以用来找可行解，或者找出全部解。找可行解的时候可以用深度优先遍历DFS，或者广度优先遍历BFS。而这个题目则是找出全部解，然后累加全部解。而搜索算法找全部解时的递归解法一般也是两种：自底向上和自顶向下（自己命名的，哈哈）。<br/>
就拿这道题来说，自底向上，也就是当递归到叶子节点后，在递归退栈的过程中，让左子树递归返回的数加上右子树递归返回的数。<br/>
注意解法中其实用到了乘法分配律，否则每次“归”的时候，就得向上层返回一个数的列表，且越接近root的时候列表会越长。或者记录一个对象内的成员变量，当遍历到叶子节点时，每个叶子节点将到达自身所形成的路径的值加上到成员变量上。<br/>

---
## 代码
``` python
class Solution:
    def doSumNumbers(self, root, val):
        if None == root.left and None == root.right:
            return val * 10 + root.val
        left = 0
        right = 0
        if None != root.left:
            left = self.doSumNumbers(root.left, val * 10 + root.val)
        if None != root.right:
            right = self.doSumNumbers(root.right, val * 10 + root.val)
        return left + right

    # @param root, a tree node
    # @return an integer
    def sumNumbers(self, root):
        if None == root:
            return 0
        return self.doSumNumbers(root, 0)
```
