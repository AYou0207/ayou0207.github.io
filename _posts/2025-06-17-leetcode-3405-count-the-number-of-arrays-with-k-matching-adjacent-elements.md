---
title: 3405. 统计恰好有 K 个相等相邻元素的数组数目
date: 2025-06-17 14:40:00 +0800
categories: [Leetcode, Math]
tags: [leetcode, math, combination]
author: ayou
description: 组合数。
comments: true
---

## 原题
[3405. 统计恰好有 K 个相等相邻元素的数组数目](https://leetcode.cn/problems/count-the-number-of-arrays-with-k-matching-adjacent-elements/description/)

## 题解
**详情**：[纯数学题（Python/Java/C++/Go）](https://leetcode.cn/problems/count-the-number-of-arrays-with-k-matching-adjacent-elements/solutions/3033292/chun-shu-xue-ti-pythonjavacgo-by-endless-mxj7)

## 代码
```python
class Solution:
    def countGoodArrays(self, n: int, m: int, k: int) -> int:
        MOD = 1_000_000_007
        return comb(n-1, k) % MOD * m * pow(m-1, n-k-1, MOD) % MOD
```
