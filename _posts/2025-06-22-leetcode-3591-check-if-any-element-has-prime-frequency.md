---
title: 3591. 检查元素频次是否为质数
date: 2025-06-22 14:25:00 +0800
categories: [Leetcode, Simulation]
tags: [leetcode, easy]
author: ayou
description: 检查数组元素出现频次是否为质数。模拟-质数-埃式筛法。
comments: true
---

## 原题
[3591. 检查元素频次是否为质数](https://leetcode.cn/problems/check-if-any-element-has-prime-frequency/description/)

## 题解
**详情**：[预处理质数](https://leetcode.cn/problems/check-if-any-element-has-prime-frequency/solutions/3705717/yu-chu-li-zhi-shu-pythonjavacgo-by-endle-rgyg)

## 代码
```python
class Solution:
    def __init__(self):
        mv = 101
        is_prime = [False] * 2 + [True] * (mv - 2)
        for i in range(2, isqrt(mv) + 1):
            if is_prime[i]:
                for j in range(i * i, mv, i):
                    is_prime[j] = False
        self.is_prime = is_prime

    def checkPrimeFrequency(self, nums: List[int]) -> bool:
        counter = Counter(nums)
        return any(
            self.is_prime[times]
            for times in counter.values()
        )
```
