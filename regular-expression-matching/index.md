# 【LeetCode with Python】 10. Regular Expression Matching
tags: Hard Problems, Dynamic Programming, Backtracking, String

## 题目
原题页面：<https://leetcode.com/problems/regular-expression-matching/><br/>
本文地址：<http://leetcode.xnerv.wang/regular-expression-matching/><br/>
题目类型：Dynamic Programming, Backtracking, String<br/>
难度评价：Hard<br/>
类似题目：[(H) Wildcard Matching](/wildcard-matching/)<br/>

> Implement regular expression matching with support for `'.'` and `'*'`.<br/>
><br/>
>> '.' Matches any single character.<br/>
>> '*' Matches zero or more of the preceding element.<br/>
>><br/>
>> The matching should cover the **entire** input string (not partial).<br/>
>><br/>
>> The function prototype should be:<br/>
>> bool isMatch(const char *s, const char *p)<br/>
>><br/>
>> Some examples:<br/>
>> isMatch("aa","a") → false<br/>
>> isMatch("aa","aa") → true<br/>
>> isMatch("aaa","aa") → false<br/>
>> isMatch("aa", "a*") → true<br/>
>> isMatch("aa", ".*") → true<br/>
>> isMatch("ab", ".*") → true<br/>
>> isMatch("aab", "c*a*b") → true<br/>

<!-- more -->

---
## 分析
和[Wildcard Matching](/wildcard-matching/)这道题类似，动态规划算法本身已经不是难点，关键在于最好对一些特殊cases做预处理：<br/>
模式串p中连续的*对可以合并成一个，如a*a*可以合并为a*，而.*.*也可以合并为.*<br/>
模式串p中实体字符（不带*）的个数大于字符串s的长度时，匹配失败<br/>
模式串p中没有任何实体字符，而字符串s长度为0时，匹配成功<br/>
此外，目前用的解法已经将使用到的DP矩阵减小到了两行，可以继续优化到2*2的小矩阵。<br/>

---
## 代码
``` python
class Solution:

    class Item:
        def __init__(self, char, symbol):
            self.char = char
            self.symbol = symbol

    def splitStr(self, str):
        items = [ ]
        index = 0
        len_str = len(str)
        while index < len_str:
            if index + 1 >= len_str or '*' != str[index + 1]:
                items.append(Solution.Item(str[index], ''))
                index += 1
            else:
                items.append(Solution.Item(str[index], '*'))
                index += 2
        return items

    # @param s, an input string
    # @param p, a pattern string
    # @return a boolean
    def isMatch(self, s, p):
        if '' == s and '' == p:
            return True
        p_arr = self.splitStr(p)
        len_s = len(s)
        len_p_arr = len(p_arr)

        last_item = Solution.Item(None, None)
        p_char_num = 0
        new_p_arr = [ ]
        for i in range(0, len_p_arr):
            if last_item.char == p_arr[i].char and last_item.symbol == p_arr[i].symbol and '*' == p_arr[i].symbol:
                pass
            else:
                new_p_arr.append(p_arr[i])
            last_item = p_arr[i]
            if '' == p_arr[i].symbol:
                p_char_num += 1
        if p_char_num > len_s:
            return False
        if 0 ==p_char_num and 0 == len_s:
            return True

        F = [[False for j in range(0, len_p_arr + 1)] for i in range(0, 2)]

        # 3 cases for True:
        #    last ch matched, and this ch matcheds (right-down)
        #    p comes x*, and last matched (right)
        #    last p.symbol is x*, s comes matched ch x, and last matched (down)
        for i in range(1, len_s + 1):
            if 1 == i:
                F[0][0] = True
                for j in range(1, len_p_arr + 1):
                    F[0][j] = (F[0][j - 1] and '*' == p_arr[j - 1].symbol)
            else:
                for j in range(0, len_p_arr + 1):          # cannot be F[0] = F[1]
                    F[0][j] = F[1][j]
            F[1][0] = False
            for j in range(1, len_p_arr + 1):
                if True == F[0][j - 1] and (p_arr[j - 1].char == s[i - 1] or '.' == p_arr[j - 1].char):
                    F[1][j] = True
                elif True == F[1][j - 1] and '*' == p_arr[j - 1].symbol:
                    F[1][j] = True
                elif True == F[0][j] and (s[i - 1] == p_arr[j - 1].char  or '.' == p_arr[j - 1].char)and '*' == p_arr[j - 1].symbol:
                    F[1][j] = True
                else:
                    F[1][j] = False

        return F[1][len_p_arr]
```
