---
title: 2787. 将一个数字表示成幂的和的方案数
date: 2025-06-22 21:45:00 +0800
categories: [Leetcode, Template]
tags: [leetcode, backpack, template]
author: ayou
description: 夯实基础-01背包问题变体。
comments: true
---

## 原题
[2787. 将一个数字表示成幂的和的方案数](https://leetcode.cn/problems/ways-to-express-an-integer-as-sum-of-powers/description/)

## 题解
**思路**：转化为数字的选取。求方案数。

**详情**：[0-1 背包模板题](https://leetcode.cn/problems/ways-to-express-an-integer-as-sum-of-powers/solutions/2354970/0-1-bei-bao-mo-ban-ti-by-endlesscheng-ap09)

## 代码
```python
class Solution:
    def numberOfWays(self, n: int, x: int) -> int:
        MOD = 1_000_000_007
        dp = [1] + [0] * n
        for i in range(1, n+1):
            w = i ** x
            if w > n:
                break
            for c in range(n, w-1, -1):
                dp[c] = (dp[c] + dp[c-w]) % MOD
        return dp[n]
```
