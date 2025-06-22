---
title: 被列覆盖的最多行数
date: 2025-06-22 17:25:00 +0800
categories: [Leetcode, Enumeration]
tags: [leetcode, enumeration, bitset]
author: ayou
description: 选取某些列，计算被这些列覆盖的行数最大是多少。子集枚举——Gosper's Hack。
comments: true
---

## 原题
[2397. 被列覆盖的最多行数](https://leetcode.cn/problems/maximum-rows-covered-by-columns/description/)

## 题解
**详情**：[两种方法：二进制枚举 / Gosper's Hack](https://leetcode.cn/problems/maximum-rows-covered-by-columns/solutions/1798794/by-endlesscheng-dvxe)

## 代码
```python
class Solution:
    def maximumRows(self, matrix: List[List[int]], numSelect: int) -> int:
        row_bits = [
            sum(x << j for j, x in enumerate(row))
            for i, row in enumerate(matrix)
        ]
        answer = 0
        limit = 1 << len(matrix[0])
        s = (1 << numSelect) - 1
        while s < limit:
            covered = sum(row & s == row for row in row_bits)
            answer = max(answer, covered)
            lowbit = s & -s
            high = s + lowbit
            low = (s ^ high) // lowbit >> 2
            s = high | low
        return answer
```
