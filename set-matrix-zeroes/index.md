# 【LeetCode with Python】 73. Set Matrix Zeroes
tags: Medium Problems, Array

## 题目
原题页面：<https://leetcode.com/problems/set-matrix-zeroes/><br/>
本文地址：<http://leetcode.xnerv.wang/set-matrix-zeroes/><br/>
题目类型：Array<br/>
难度评价：Medium<br/>
类似题目：[(M) Game of Life](/game-of-life/)<br/>

> Given a *m* x *n* matrix, if an element is 0, set its entire row and column to 0. Do it in place.<br/>
><br/>
> **Follow up:**<br/>
> Did you use extra space?<br/>
> A straight forward solution using O(*m**n*) space is probably a bad idea.<br/>
> A simple improvement uses O(*m* + *n*) space, but still not the best solution.<br/>
> Could you devise a constant space solution?<br/>

<!-- more -->

---
## 分析
看到这题的第一个想到的最简单的算法是，做一次m*n的遍历，每次遇到0，就将所在的行和列的元素给清零了，显然这样可能大量的重复清零。<br/>
然后想到的是，不应该在遍历的过程中就开始清零，而是应该记录下应该清零哪些行和列，这样再遍历完成后再一次性地完成清零工作。于是就需要空间来记录所有行和列是否需要清零。<br/>
但是题目又要求不能使用额外空间，于是就只可能用原有的矩阵来进行记录。如果一个点(x,y)=0，则将(x,0)和(0,y)标记为0，表示第x列和第y行需要清零。<br/>
但是，假如第二行的第一个元素是0，则会导致(0,0)标记为0，这样会使得第一行和第一列被清零，显然此时第一行被清零是不应该的。我这里采用的做法是，对于第一行和第一列是否需要清零，用两个额外的变量来标记。我尝试了很久，希望能通过使用点(m-1,n-1)，从而去除掉这两个额外变量，但试了很久都没有实现，以后还会继续思考是否可行。不过因为题目要求的是常量空间，所以现在这种算法已经符合要求了。<br/>

---
## 代码
``` python
class Solution:
    # @param matrix, a list of lists of integers
    # RETURN NOTHING, MODIFY matrix IN PLACE.
    def setZeroes(self, matrix):
        if None == matrix or [ ] == matrix or None == matrix[0] or [ ] == matrix[0]:
            return
        firstrow_clear = False    ###
        firstcol_clear = False
        len_x = len(matrix)
        len_y = len(matrix[0])
        for i in range(0, len_x):
            for j in range(0, len_y):
                if 0 == matrix[i][j]:
                    matrix[i][0] = 0
                    matrix[0][j] = 0
                    if 0 == i:
                        firstrow_clear =  True
                    if 0 == j:
                        firstcol_clear = True
        for i in range(1, len_x):
            if 0 == matrix[i][0]:
                for j in range(0, len_y):
                    matrix[i][j] = 0
        for j in range(1, len_y):
            if 0 == matrix[0][j]:
                for i in range(0, len_x):
                    matrix[i][j]  = 0
        if firstcol_clear:
            for i in range(1, len_x):
                matrix[i][0] = 0
        if firstrow_clear:
            for j in range(1, len_y):
                matrix[0][j] = 0
```
