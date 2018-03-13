# 【LeetCode with Python】 151. Reverse Words in a String
tags: Medium Problems, String

## 题目
原题页面：<https://leetcode.com/problems/reverse-words-in-a-string/><br/>
本文地址：<http://leetcode.xnerv.wang/reverse-words-in-a-string/><br/>
题目类型：Medium<br/>
难度评价：String<br/>
类似题目：[(M) Reverse Words in a String II](/reverse-words-in-a-string-ii/)<br/>

> Given an input string, reverse the string word by word.<br/>
><br/>
> For example,<br/>
> Given s = "`the sky is blue`",<br/>
> return "`blue is sky the`".<br/>
><br/>
> **<font color="red">Update (2015-02-12):</font>**<br/>
> For C programmers: Try to solve it *in-place* in *O*(1) space.<br/>
><br/>
> **Clarification:**<br/>
><br/>
> * What constitutes a word?<br/>
> A sequence of non-space characters constitutes a word.<br/>
> * Could the input string contain leading or trailing spaces?<br/>
> Yes. However, your reversed string should not contain leading or trailing spaces.<br/>
> * How about multiple spaces between two words?<br/>
> Reduce them to a single space in the reversed string.<br/>

<!-- more -->

---
## 分析
反转一句话中的单词。注意题中还要求去除首尾可能存在的空白字符，词与词之间也要去除多余空白字符，而只留一个空白。<br/>

---
## 代码
``` python
class Solution:

    # @param s, a string
    # @return a string
    def reverseWords(self, s):

        len_s = len(s)
        if len_s < 1:
            return s

        index_right = len_s - 1
        new_s = ""

        while index_right >= 0:
            while index_right >= 0 and ' ' == s[index_right]:
                index_right -= 1
            end_index = index_right
            while index_right >= 0 and ' ' != s[index_right]:
                index_right -= 1
            start_index = index_right + 1
            word = s[start_index : end_index + 1] if end_index >= 0 else ""
            new_s += (word + " ")

        return new_s.rstrip()
```
