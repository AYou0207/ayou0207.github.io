---
title: 2138. 将字符串拆分为若干长度为 k 的组
date: 2025-06-22 01:35:00 +0800
categories: [Leetcode, Simulation]
tags: [leetcode, easy]
author: ayou
description: 按照要求对字符串进行处理。模拟。
comments: true
---

## 原题
[2138. 将字符串拆分为若干长度为 k 的组](https://leetcode.cn/problems/divide-a-string-into-groups-of-size-k/)

## 题解
**详情**：[简单题，简单做](https://leetcode.cn/problems/divide-a-string-into-groups-of-size-k/solutions/1213950/go-mo-ni-by-endlesscheng-tv8c)

## 代码
```python
class Solution:
    def divideString(self, s: str, k: int, fill: str) -> List[str]:
        n = len(s)
        return [
            s[i:i+k] + fill * (k-n+i)
            for i in range(0, n, k)
        ]
```
