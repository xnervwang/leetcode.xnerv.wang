# 【LeetCode with Python】 14. Longest Common Prefix
tags: Easy Problems, String

## 题目
原题页面：<https://leetcode.com/problems/longest-common-prefix/><br/>
本文地址：<<leetcode-with-python-domain>/longest-common-prefix/><br/>
题目类型：String<br/>
难度评价：Easy<br/>

> Write a function to find the longest common prefix string amongst an array of strings.<br/>

<!-- more -->

---
## 分析
很简单的题目，找一堆字符串的最长公共前缀。先找str1和str2的最长公共前缀例如str1_2，再找str1_2和str3的最长公共前缀str1_2_3……<br/>

---
## 代码
``` python
class Solution:

    def findPrefix(self, str1, str2):
        min_len = min(len(str1), len(str2))
        for i in range(0, min_len):
            if str1[i] != str2[i]:
                return str1[0:i]
        return str1[0:min_len]

    # @return a string
    def longestCommonPrefix(self, strs):
        if None == strs:
            return ""
        n = len(strs)
        if 0 == n:
            return ""
        elif 1 == n:
            return strs[0]

        prefix = strs[0]
        for str in strs[1:]:
            prefix = self.findPrefix(prefix, str)
            if "" == prefix:
                break
        return prefix
```
