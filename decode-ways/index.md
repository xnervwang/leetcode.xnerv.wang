# 【LeetCode with Python】 91. Decode Ways
tags: Medium Problems, Dynamic Programming, String

## 题目
原题页面：<https://leetcode.com/problems/decode-ways/><br/>
本文地址：<http://leetcode.xnerv.wang/decode-ways/><br/>
题目类型：Dynamic Programming, String<br/>
难度评价：Medium<br/>

> A message containing letters from `A-Z` is being encoded to numbers using the following mapping:<br/>
><br/>
>     'A' -> 1<br/>
>     'B' -> 2<br/>
>     ...<br/>
>     'Z' -> 26<br/>
><br/>
> Given an encoded message containing digits, determine the total number of ways to decode it.<br/>
><br/>
> For example,<br/>
> Given encoded message `"12"`,<br/>
> it could be decoded as `"AB"` (1 2) or `"L"` (12).<br/>
><br/>
> The number of ways decoding `"12"` is 2.<br/>

<!-- more -->

---
## 分析
（这个应该是一个一维DP问题，本质是裴波拉契数列，为什么我用了两行？？？）<br/>
DP问题，需要注意的除了边界条件的处理，还有关于'0'的注意点。'0'本身可以构成'10'，'20'这样合法的双字节码，但其它情况的'0'就是异常数据了。**这道题目跟atoi一样，都属于题意描述不清晰，题意本身并没有说清楚要“尽量多地解码出字符串”**，因此一开始我一旦发现有多余的'0'就直接认为解码失败范围0，结果提交后发现不对。此外，**输入的参数s也可能是个空串，从验证的结果看来这种情况下应该返回0，题目也没有说清楚**。<br/>
另外对于很大一部分DP题目，内存都是可以优化的，这里也不必采用n * 2大小的二维数组，只需保留两行，即2 * 2的空间消耗即可。<br/>
最后，还要特别说明一下新学到的一招。起先还想像C语言一样写个swap函数，用一个临时变量tmp来交换solu_arr1和solu_arr2两个引用，后来发现竟然可以用solu_arr1, solu_arr2 = solu_arr2, solu_arr1这种简便的写法，大赞Python！（同时也说明了我学Python是半路出家……）<br/>

---
## 代码
``` python
class Solution:
    # @param s, a string
    # @return an integer
    def numDecodings(self, s):
        if None == s or 0 == len(s) or '0' == s[0]:
            return 0
        solu_arr1 = [0, 1]
        solu_arr2 = [0, 0]
        for i in range(1, len(s) + 1):
            cur_ch = s[i - 1]
            last_ch = s[i - 2] if 1 != i else ''
            if cur_ch >= '1' and cur_ch <= '9':
                solu_arr2[0] = solu_arr1[0] + solu_arr1[1]
            else:
                solu_arr2[0] = 0
            double_ch = last_ch + cur_ch
            if '' == last_ch or '0' == last_ch or int(double_ch) > 26:
                solu_arr2[1] = 0
            else:
                solu_arr2[1] = solu_arr1[0]
            solu_arr1, solu_arr2 = solu_arr2, solu_arr1    # swap

        return solu_arr1[0] + solu_arr1[1]
```
