---
title: 字符串解码
date: 2025-06-16 12:10:00 +0800
categories: [Leetcode, Stack]
tags: [leetcode, stack, medium]
author: ayou
description: 解码特定规则下的字符串。栈 & 递归。
comments: true
---

## 原题
[394. 字符串解码](https://leetcode.cn/problems/decode-string/description/)

## 题解
**详情**：[栈 & 递归](https://leetcode.cn/problems/decode-string/solutions/3701261/zhan-di-gui-by-wrran-nfu1)

## 代码
```python
class Solution:
    def decodeString(self, s: str) -> str:
        n = len(s)
        def decode(i):
            # i 记录当前解析位置

            # answer 记录当前解码出来的字符串
            # num 记录当前解码出来字符串的重复次数
            answer, num = "", 0
            while i < n:
                if s[i].isdigit():
                    num = num * 10 + int(s[i])
                elif s[i] == '[':
                    i, nested = decode(i+1)
                    answer += num * nested
                    num = 0
                elif s[i] == ']':
                    return i, answer
                else:
                    answer += s[i]
                i += 1
            return n, answer

        return decode(0)[1]
```
