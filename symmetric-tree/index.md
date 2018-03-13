# 【LeetCode with Python】 101. Symmetric Tree
tags: Easy Problems, Tree, Depth-first Search

## 题目
原题页面：<https://leetcode.com/problems/symmetric-tree/><br/>
本文地址：<http://leetcode.xnerv.wang/symmetric-tree/><br/>
题目类型：Tree, Depth-first Search<br/>
难度评价：Easy<br/>

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).<br/>

For example, this binary tree is symmetric:<br/>
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following is not:<br/>
```
    1
   / \
  2   2
   \   \
   3    3
```

**Note:**<br/>
Bonus points if you could solve it both recursively and iteratively.<br/>

confused what `"{1,#,2,3}"` means?

**OJ's Binary Tree Serialization:**<br/>
The serialization of a binary tree follows a level order traversal, where '#' signifies a path terminator where no node exists below.

Here's an example:<br/>
```
   1
  / \
 2   3
    /
   4
    \
     5
```
The above binary tree is serialized as `"{1,2,3,#,#,4,#,#,5}"`.

<!-- more -->

---
## 分析
最开始想到的方法是进行二叉树的层次遍历，判断每一层的节点列表是不是左右对称的。但题目建议用递归回溯，但是如何在递归中判断对称的确不容易想到。<br/>
就这道题目而言，其实也是递归地判断每组对称的两点是否相等。<br/>

---
## 代码
``` python
class Solution:

    def checkSysmmetric(self, left, right):
        if None == left and None == right:
            return True
        elif None == left or None == right:
            return False
        elif left.val != right.val:
            return False
        return self.checkSysmmetric(left.left, right.right) and self.checkSysmmetric(left.right, right.left)

    # @param root, a tree node
    # @return a boolean
    def isSymmetric(self, root):
        if None == root:
            return True
        return self.checkSysmmetric(root.left, root.right)
```
