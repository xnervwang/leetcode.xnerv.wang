# 【LeetCode with Python】 97. Interleaving String
tags: Hard Problems, Dynamic Programming, String

## 题目
原题页面：<https://leetcode.com/problems/interleaving-string/><br/>
本文地址：<http://leetcode.xnerv.wang/interleaving-string/><br/>
题目类型：Dynamic Programming, String<br/>
难度评价：Hard<br/>

> Given *s1*, *s2*, *s3*, find whether *s3* is formed by the interleaving of *s1* and *s2*.<br/>
><br/>
> For example,<br/>
> Given:<br/>
> *s1* = `"aabcc"`,<br/>
> *s2* = `"dbbca"`,<br/>
><br/>
> When *s3* = `"aadbbcbcac"`, return true.<br/>
> When *s3* = `"aadbbbaccc"`, return false.<br/>

<!-- more -->

---
## 分析
比较常规的一道字符串DP问题。注意检查传入参数，可以加速某些极端case的检测速度。此外还可以用两个row代替一个完整的二维矩阵，节约空间消耗。<br/>

---
## 代码
``` python
class Solution:

    # @return a boolean
    def isInterleave(self, s1, s2, s3):
        len1 = len(s1)
        len2 = len(s2)
        len3 = len(s3)

        if len1 + len2 != len3:
            return False
        if 0 == len1:
            return s2 == s3
        if 0 == len2:
            return s1 == s3

        row1 = [False for col in range(len2 + 1)]
        row1[0] = True
        for i in range(1, len2 + 1):
            row1[i] = ( row1[i - 1] and (s2[i - 1] == s3[i - 1]))

        row2 = [False for col in range(len2 + 1)]

        for m in range(1, len1 + 1):
            row2[0] = (row1[0] and (s1[m - 1] == s3[m - 1]))
            for n in range(1, len2 + 1):
                k = m + n - 1
                # why and ? because [m, n] maybe come from up or left, one of the two is the right source.
                row2[n] = (s1[m - 1] == s3[k] and row1[n]) or (s2[n - 1] == s3[k] and row2[n - 1])
            row1, row2 = row2, row1

        return row1[len2]
```
