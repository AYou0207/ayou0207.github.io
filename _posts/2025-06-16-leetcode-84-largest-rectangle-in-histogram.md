---
title: 柱状图中最大的矩形
date: 2025-06-16 15:50:00 +0800
categories: [Leetcode, MonoStack]
tags: [leetcode, monostack, medium]
author: ayou
description: 记录每个位置的左右小于当前位置的位置。单调栈。
comments: true
---

## 原题
[84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/description/)

## 题解
**思路**：通过两个单调栈分别维护每个位置左边以及右边第一个小于当前高度的位置，之后计算最大面积。

**详情**：[一步步优化：从三次遍历到一次遍历（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/largest-rectangle-in-histogram/solutions/2695467/dan-diao-zhan-fu-ti-dan-pythonjavacgojsr-89s7)

## 代码
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        n = len(heights)

        left = [-1] * n
        stk = []
        for i, h in enumerate(heights):
            while stk and h <= heights[stk[-1]]:
                stk.pop()
            if stk:
                left[i] = stk[-1]
            stk.append(i)
        
        right = [n] * n
        stk = []
        for i in range(n-1, -1, -1):
            h = heights[i]
            while stk and h <= heights[stk[-1]]:
                stk.pop()
            if stk:
                right[i] = stk[-1]
            stk.append(i)

        answer = 0
        for h, l, r in zip(heights, left, right):
            answer = max(answer, h * (r - l - 1))
        return answer
```
