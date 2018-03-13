# 【LeetCode with Python】 44. Wildcard Matching
tags: Hard Problems, Dynamic Programming, Backtracking, Greedy, String

## 题目
原题页面：<https://leetcode.com/problems/wildcard-matching/><br/>
本文地址：<<leetcode-with-python-domain>/wildcard-matching/><br/>
题目类型：Dynamic Programming, Backtracking, Greedy, String<br/>
难度评价：Hard<br/>
类似题目：[ (H) Regular Expression Matching](/regular-expression-matching/)<br/>

> Implement wildcard pattern matching with support for `'?'` and `'*'`.<br/>
><br/>
>     '?' Matches any single character.<br/>
>     '*' Matches any sequence of characters (including the empty sequence).<br/>
><br/>
>     The matching should cover the **entire** input string (not partial).<br/>
><br/>
>     The function prototype should be:<br/>
>     bool isMatch(const char *s, const char *p)<br/>
><br/>
>     Some examples:<br/>
>     isMatch("aa","a") → false<br/>
>     isMatch("aa","aa") → true<br/>
>     isMatch("aaa","aa") → false<br/>
>     isMatch("aa", "*") → true<br/>
>     isMatch("aa", "a*") → true<br/>
>     isMatch("ab", "?*") → true<br/>
>     isMatch("aab", "c*a*b") → false<br/>

<!-- more -->

---
## 分析
这道动态规划的题，其特殊test case造成的麻烦已经远远超过动态规划算法本身的复杂带来的麻烦了。之前在优化动态规划算法时，一直注重的是空间的优化，却没有考虑到有些cases是可以提前检测或进行预处理，从而降低运行时间的。如果不这样做，将一直卡在一些特别长的变态cases上Time Limit Exceeded。<br/>
1. 模式串p中连续的*可以预处理合并为一个*<br/>
2. 模式串中问号和字符的总数大于字符串s的长度时，匹配失败<br/>
3. 模式串中字符个数为0时，如果模式串中问号总数等于s长度，则匹配成功，否则匹配失败<br/>

---
## 代码
``` python
class Solution:
    # @param s, an input string
    # @param p, a pattern string
    # @return a boolean
    def isMatch(self, s, p):
        if (None == s or '' == s) and (None == p or '' == p):
            return True
        len_s = len(s)
        len_p = len(p)
        new_p = ''
        last_ch = None
        p_solid_char_num = 0
        for i in range(0, len_p):
            if '*' != last_ch or '*' != p[i]:
                new_p += p[i]
            last_ch = p[i]
            if '*' != p[i]:
                p_solid_char_num += 1
        if p_solid_char_num > len_s:
            return False
        isAllStars = True
        if (None == s or '' == s) and 0 == p_solid_char_num:
                return True
        p = new_p
        len_p = len(new_p)

        F = [[False for j in range(0, len_p + 1)] for i in range(0, 2)]

        # 3 cases for True:
        #    last ch matched, and this ch matcheds (right-down)
        #    p comes *, and last matched (right)
        #    last p.ch is *, s comes any ch, and last matched (down)
        for i in range(1, len_s + 1):
            if 1 == i:
                F[0][0] = True
                for j in range(1, len_p + 1):
                    F[0][j] = (F[0][j - 1] and '*' == p[j - 1])
            else:
                for j in range(0, len_p + 1):          # cannot be F[0] = F[1]
                    F[0][j] = F[1][j]
            F[1][0] = False
            for j in range(1, len_p + 1):
                if True == F[0][j - 1] and (p[j - 1] == s[i - 1] or '?' == p[j - 1] or '*' == p[j - 1]):
                    F[1][j] = True
                elif (True == F[1][j - 1] or True == F[0][j]) and '*' == p[j - 1]:
                    F[1][j] = True
                else:
                    F[1][j] = False

        return F[1][len_p]
```
