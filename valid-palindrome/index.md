# 【LeetCode with Python】 125. Valid Palindrome
tags: Easy Problems, Two Pointers, String

## 题目
原题页面：<https://leetcode.com/problems/valid-palindrome/><br/>
本文地址：<http://leetcode.xnerv.wang/valid-palindrome/><br/>
题目类型：Two Pointers, String<br/>
难度评价：Easy<br/>
类似题目：[(E) Palindrome Linked List](/palindrome-linked-list/)<br/>

> Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.<br/>
><br/>
> For example,<br/>
> `"A man, a plan, a canal: Panama"` is a palindrome.<br/>
> `"race a car"` is *not* a palindrome.<br/>
><br/>
> **Note:**<br/>
> Have you consider that the string might be empty? This is a good question to > ask during an interview.<br/>
><br/>
> For the purpose of this problem, we define empty string as valid palindrome.<br/>

<!-- more -->

---
## 分析
判断一个字符串是否为回文，忽略字母和数字外的字符，忽略字母大小写，并且注意检测作为参数传入的字符串是否为空串。这可能就是面试时的编程题与ACM赛题的最大区别之一：需要考虑各种异常情形和边界条件，题目虽简单，面试官考察的是应试者整体的编程思维，而不仅仅是具体某个精妙的算法。<br/>

---
## 代码
``` python
class Solution:

    # @param s, a string
    # @return a boolean
    def isPalindrome(self, s):
        len_s = len(s)
        if len_s <= 1:
            return True

        left_idx = 0
        right_idx = len_s - 1
        is_match = True
        while left_idx < right_idx:

            if (False == ((s[left_idx] >= 'a' and s[left_idx] <= 'z') or (s[left_idx] >= 'A' and s[left_idx] <= 'Z')\
				or (s[left_idx] >= '0' and s[left_idx] <= '9'))):
                left_idx += 1
                continue
            left_chr = (chr(ord(s[left_idx]) - ord('A') + ord('a'))\
				if (s[left_idx] >= 'A' and s[left_idx] <= 'Z') else s[left_idx])

            if (False == ((s[right_idx] >= 'a' and s[right_idx] <= 'z') or (s[right_idx] >= 'A' and s[right_idx] <= 'Z')\
				or (s[right_idx] >= '0' and s[right_idx] <= '9'))):
                right_idx -= 1
                continue
            right_chr = (chr(ord(s[right_idx]) - ord('A') + ord('a'))\
				if (s[right_idx] >= 'A' and s[right_idx] <= 'Z') else s[right_idx])

            if left_chr == right_chr:
                left_idx += 1
                right_idx -= 1
            else:
                is_match = False
                break

        return is_match
```
