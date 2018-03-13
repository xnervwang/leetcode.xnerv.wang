# 【LeetCode with Python】 72. Edit Distance
tags: Hard Problems, Dynamic Programming, String

## 题目
原题页面：<https://leetcode.com/problems/edit-distance/><br/>
本文地址：<<leetcode-with-python-domain>/edit-distance/><br/>
题目类型：Dynamic Programming, String<br/>
难度评价：Hard<br/>
类似题目：[(M) One Edit Distance](/one-edit-distance/)<br/>

> Given two words *word1* and *word2*, find the minimum number of steps required to convert *word1* to *word2*. (each operation is counted as 1 step.)<br/>
><br/>
> You have the following 3 operations permitted on a word:<br/>
><br/>
> a) Insert a character<br/>
> b) Delete a character<br/>
> c) Replace a character<br/>

<!-- more -->

---
## 分析
一道传统意义上的经典的动态规划题目。注意动态规划十有八九可以优化空间复杂度，不是真的要开辟一个(m+1)*(n+1)的大矩阵出来。目前用的解法已经减小到了两行，可以继续优化到2*2的小矩阵。<br/>
对于这个DP矩阵，每个方格代表当前子问题的最佳解决方案。如果每个方格记录下自身是基于如何从上一层子问题的最佳解决方案推进而来，则通过这层线索，可以从指定的一个方格，反向推演出当前最佳方案的整个构成路径。如果一个方法的最佳解决方案不只一个，则构成路径变成了一棵树。<br/>
DP矩阵的第0行和第0列一般都要特别处理。<br/>
此外，DP的题目最好能习惯于写出DP递推方程，这样可以用更简洁的公式来解释思路：<br/>
1. d[0, j] = j<br/>
2. d[i, 0] = i<br/>
3. d[i, j] = d[i-1, j - 1] if A[i] == B[j]<br/>
4. d[i, j] = min(d[i-1, j - 1], d[i, j - 1], d[i-1, j]) + 1  if A[i] != B[j]<br/>

---
## 代码
``` python
class Solution:
    # @return an integer
    def minDistance(self, word1, word2):
        if "" == word1 and "" == word2:
            return 0
        elif "" == word1:
            return len(word2)
        elif "" == word2:
            return len(word1)
        len1 = len(word1)
        len2 = len(word2)
        arr1 = [0 for y in range(0, len1 + 1)]
        arr2 = [0 for y in range(0, len1 + 1)]
        arr1[0] = 0
        for y in range(1, len1 + 1):
            arr1[y] = y
        for x in range(1, len2 + 1):
            arr2[0] = x
            for y in range(1, len1 + 1):
                arr2[y] = min(arr1[y - 1] + (0 if (word1[y - 1] == word2[x - 1]) else 1), arr1[y] + 1, arr2[y - 1] + 1)
            tmp = arr1
            arr1 = arr2
            arr2 = tmp
            for y in range(0, len1 + 1):
                arr2[y] = 0
        return arr1[len1]
```
