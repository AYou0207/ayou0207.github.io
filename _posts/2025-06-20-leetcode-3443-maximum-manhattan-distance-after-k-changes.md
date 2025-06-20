---
title: K 次修改后的最大曼哈顿距离
date: 2025-06-20 16:30:00 +0800
categories: [Leetcode, Greedy]
tags: [leetcode, greedy]
author: ayou
description: 修改行动路径中的 K 步，求离原点最远的曼哈顿距离。贪心。
comments: true
---

## 原题
[3443. K 次修改后的最大曼哈顿距离](https://leetcode.cn/problems/maximum-manhattan-distance-after-k-changes/description/)

## 题解
**详情**：[两种方法（Python/Java/C++/Go）](https://leetcode.cn/problems/maximum-manhattan-distance-after-k-changes/solutions/3061765/heng-zong-zuo-biao-fen-bie-ji-suan-tan-x-lhhi)

## 代码
```python
class Solution:
    def maxDistance(self, s: str, k: int) -> int:
        answer = x = y = 0
        for i, ch in enumerate(s):
            if ch == "N":
                y += 1
            elif ch == "S":
                y -= 1
            elif ch == "E":
                x += 1
            else:
                x -= 1
            answer = max(
                answer, min(abs(x) + abs(y) + k * 2, i+1)
            )
        return answer
```
