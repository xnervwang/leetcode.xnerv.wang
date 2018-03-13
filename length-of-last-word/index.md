# 【LeetCode with Python】 58. Length of Last Word
tags: Easy Problems, String

## 题目
原题页面：<https://leetcode.com/problems/length-of-last-word/><br/>
本文地址：<http://leetcode.xnerv.wang/length-of-last-word/><br/>
题目类型：String<br/>
难度评价：Easy<br/>

> Given a string *s* consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word in the string.<br/>
><br/>
> If the last word does not exist, return 0.<br/>
><br/>
> **Note:** A word is defined as a character sequence consists of non-space characters only.<br/>
><br/>
> For example,<br/>
> Given *s* = `"Hello World"`,<br/>
> return `5`.<br/>

<!-- more -->

---
## 分析
计算一句话中最后一个单词的长度。这道题很简单，但陷阱就在于要注意处理好一些异常或边界情形，如空串，最后一个单词后面还有空白等等。<br/>

---
## 代码
``` python
class Solution:

    # @param s, a string
    # @return an integer
    def lengthOfLastWord(self, s):

        len_s = len(s)
        if 0 == len_s:
            return 0

        index = len_s - 1
        while index >= 0 and ' ' == s[index]:
            index -= 1
        len_last_word = 0
        while index >= 0 and ' ' != s[index]:
            len_last_word += 1
            index -= 1
        return len_last_word
```
