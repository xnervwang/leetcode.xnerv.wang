# 【LeetCode with Python】 112. Path Sum
tags: Easy Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/path-sum/><br/>
本文地址：<http://leetcode.xnerv.wang/path-sum/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Easy<br/>
类似题目：[(M) Path Sum II](/path-sum-ii/), [(H) Binary Tree Maximum Path Sum](/binary-tree-paths/), [(M) Sum Root to Leaf Numbers](sum-root-to-leaf-numbers)<br/>

> Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.<br/>
><br/>
> For example:<br/>
> Given the below binary tree and `sum = 22`,<br/>
><br/>
>                   5<br/>
>                  / \<br/>
>                 4   8<br/>
>                /   / \<br/>
>               11  13  4<br/>
>              /  \      \<br/>
>             7    2      1<br/>
><br/>
> return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.<br/>

<!-- more -->

---
## 分析
简单的递归算法。但是注意一点，当树为空树时，无论sum是多少都一定要返回False，即使此时sum为0。另外因为只要确定有解即可，因此如果某次迭代发现left已经找到解，那么就不需要再去右子树中寻找解。<br/>
但是，因为可能有负数出现，所以不能因为path sum已经大于指定sum值就认为该分支可以被剪除。<br/>

---
## 代码
``` python
class Solution:

    def doHasPathSum(self, root, total, sum):
        if None == root.left and None == root.right:
            return sum == (total + root.val)

        left= False
        right = False
        if None != root.left:
            left = self.doHasPathSum(root.left, total + root.val, sum)
        if False != left and None != root.right:     # pruning
            right = self.doHasPathSum(root.right, total + root.val, sum)
        return left or right

    # @param root, a tree node
    # @param sum, an integer
    # @return a boolean
    def hasPathSum(self, root, sum):
        if None == root:
            return False ###
        return self.doHasPathSum(root, 0, sum)
```
