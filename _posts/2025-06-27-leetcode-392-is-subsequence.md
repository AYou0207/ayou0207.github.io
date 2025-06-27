---
title: 判断子序列
date: 2025-06-27 22:10:00 +0800
categories: [Leetcode, Subsequence]
tags: [leetcode, subsequence, template]
author: ayou
description: 子序列判定。夯实基础
comments: true
---

## 原题
[392. 判断子序列](https://leetcode.cn/problems/is-subsequence/description/)

## 题解
**详情**：[简洁写法，附进阶问题解答](https://leetcode.cn/problems/is-subsequence/solutions/2813031/jian-ji-xie-fa-pythonjavaccgojsrust-by-e-mz22)

## 代码
```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        it = iter(t)
        return all(
            # 检查其每一个位置都出现在 源字符串 s
            # 注意此处 要使用迭代器
            ch in it
            # 实质上，是要匹配字符串 s
            for ch in s
        )
```
