---
title: 50. Pow(x, n)
date: 2025-06-17 14:20:00 +0800
categories: [Leetcode, Template]
tags: [leetcode, template, pow]
author: ayou
description: 快速幂。
comments: true
---

## 原题
[50. Pow(x, n)](https://leetcode.cn/problems/powx-n/description/)

## 题解
**详情**：[【图解】一张图秒懂快速幂！（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/powx-n/solutions/2858114/tu-jie-yi-zhang-tu-miao-dong-kuai-su-mi-ykp3i)

## 代码
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        answer = 1
        if n < 0:
            n = -n
            x = 1 / x
        while n:
            if n & 1:
                answer *= x
            x *= x
            n >>= 1
        return answer
```
