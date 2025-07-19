---
title: 739. 每日温度
date: 2025-06-16 13:20:00 +0800
categories: [Leetcode, MonoStack]
tags: [leetcode, monostack, medium]
author: ayou
description: 解码特定规则下的字符串。单调栈。
comments: true
---

## 原题
[739. 每日温度](https://leetcode.cn/problems/daily-temperatures/description/)

## 题解
**思路**：单调栈中维持温度最高且距离 `i` 最近的位置。

**详情**：[单调栈](https://leetcode.cn/problems/daily-temperatures/solutions/2470179/shi-pin-jiang-qing-chu-wei-shi-yao-yao-y-k0ks)

## 代码
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        n = len(temperatures)
        answer = [0] * n
        stk = []
        for i in range(n-1, -1, -1):
            t = temperatures[i]
            while stk and t >= temperatures[stk[-1]]:
                stk.pop()
            if stk:
                answer[i] = stk[-1] - i
            stk.append(i)
        return answer
```
