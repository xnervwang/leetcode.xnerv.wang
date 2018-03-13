# 【LeetCode with Python】 93. Restore IP Addresses
tags: Medium Problems, Backtracking, String

## 题目
原题页面：<https://leetcode.com/problems/restore-ip-addresses/><br/>
本文地址：<<leetcode-with-python-domain>/restore-ip-addresses/><br/>
题目类型：Backtracking, String<br/>
难度评价：Medium<br/>

> Given a string containing only digits, restore it by returning all possible valid IP address combinations.<br/>
><br/>
> For example:<br/>
> Given `"25525511135"`,<br/>
><br/>
> return `["255.255.11.135", "255.255.111.35"]`. (Order does not matter)<br/>

<!-- more -->

---
## 分析
（这道题可以用DP来解答么？？？）<br/>
搜索，递归，剪枝。<br/>
注意剪枝条件：1.每个域的数值不能大于255；2.有且刚好4个域；3.一个域的长度>=2时，不能以0开头。因此逻辑结构如下：<br/>

1. 如果当前考察字符不是最后一个字符<br/>
1. 如果当前字符附加到当前已有数据域（num）后面，数据域新值不大于255时<br/>
1. 如果当前出现的小数点数目（fields）小于3，则可以考虑直接在已有前缀（prefix）后面加一个小数点，然后以当前字符开头，开始新的数据域<br/>
2. 如果当前已有数据域不是0，则可以考虑将本字符直接附加到当前已有数据域<br/>
2 否则，就看当前小数点数目是不是小于3，小于就可以考虑直接在已有前缀（prefix）后面加一个小数点，然后以当前字符开头，开始新的数据域<br/>
3. 否则则本分支失败<br/>
2. 如果当前考察字符是最后一个字符<br/>
1. 如果当前已有有三个小数点，当前数据域不是0，并且将当前字符附加到当前数据域后面，数据域新值也不会大于255时，可以考虑这样做<br/>
2. 否则如果当前已有两个小数点，则用小数点结束当前数据域，然后以当前字符作为最后一个数据域从而构成一个解<br/>
3. 否则当前分支失败<br/>

---
## 代码
``` python
class Solution:

    def doRestoreIpAddresses(self, prefix, num, s, start, fields):
        if start == len(s) - 1:
            results1 = [ ]
            results2 = [ ]
            if int(num + s[start]) <= 255 and 3 == fields and '0' != num:
                results1 = [prefix + s[start]]
            elif 2 == fields:
                results2 = [prefix + '.' + s[start]]
            return results1 + results2
        if int(num + s[start]) <= 255:
            results0 = [ ]
            results1 = [ ]
            if fields < 3:
                results0 = self.doRestoreIpAddresses(prefix + '.' + s[start], s[start], s, start + 1, fields + 1)
            if '0' != num:
                results1 = self.doRestoreIpAddresses(prefix + s[start], num + s[start], s, start + 1, fields)
            return results0 + results1
        elif fields < 3:
            results0 = self.doRestoreIpAddresses(prefix + '.' + s[start], s[start], s, start + 1, fields + 1)
            return results0
        else:
            return [ ]

    # @param s, a string
    # @return a list of strings
    def restoreIpAddresses(self, s):
        if len(s) < 4:
            return [ ]
        return self.doRestoreIpAddresses(s[0], s[0], s, 1, 0)
```
