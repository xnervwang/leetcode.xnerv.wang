# 【LeetCode with Python】 7. Reverse Integer
tags: Easy Problems, Math

## 题目
原题页面：<https://leetcode.com/problems/reverse-integer/><br/>
本文地址：<http://leetcode.xnerv.wang/reverse-integer/><br/>
题目类型：Math<br/>
难度评价：Easy<br/>
类似题目：[(E) String to Integer (atoi)](/string-to-integer-atoi/)<br/>

> Reverse digits of an integer.<br/>
><br/>
> **Example1:** x =  123, return  321<br/>
> **Example2:** x = -123, return -321<br/>
><br/>
> **Have you thought about this?**<br/>
><br/>
> Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!<br/>
><br/>
> If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.<br/>
><br/>
> Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?<br/>
><br/>
> For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.<br/>
><br/>
> **<font color="red">Update (2014-11-10):</font>**<br/>
> Test cases had been added to test the overflow behavior.<br/>

<!-- more -->

---
## 分析
“反转”一个数字。主要注意负数的处理。数值计算类面试题有一个经常会被忽略的重要点，就是数值溢出。这里是用Python解题，所以对于超出int范围的输入参数处理还不会有问题。但是题目要求在int溢出的情况下返回0，因此要注意检查输入，并且在反转的过程中时刻检查是否溢出。<br/>
此外还要注意Python的一个坑，之前直接用的sys.maxint来表示int最大值，在64位win7上结果正确，但在leetcode网站上跑时就出错了，发现是因为sys.maxint在windows上是32位，而在linux上则是64位，官方文档上说的也是 "<span style="color: red">This is at least 2**31-1</span>"。<br/>

---
## 代码
``` python
class Solution:
    # @return an integer
    def reverse(self, x):
        if x > 0x7fffffff or x < -0x80000000:
            return 0
        elif x >= 0:
            leave = x
            sign = 1
        else:
            leave = -x
            sign = -1

        result = 0
        while 0 != leave:
            result = result * 10 + leave % 10
            sign_result = result * sign
            if sign_result > 0x7fffffff or sign_result < -0x80000000:
                return 0
            leave /= 10
        return result * sign
```
