---
title: 1049. 最后一块石头的重量 II
date: 2025-06-24 13:45:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack]
author: ayou
description: 从一堆石头中不停地选取两块石头进行粉碎，问最后一块石头最小重量为多少。01 背包。
comments: true
---

## 原题
[1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii/description/)

## 题解
**思路**：该题难点在于识别可以转换为 01背包问题。

不失一般性，我们考虑两块石头$a$及$b$，且$a\ge b$。第一次取出这两块石头，剩余 $a-b$ 放回石堆。下一次取出剩余部分时，可能比另一块石头更大，则相当于 $+(a-b)-x$；否则，相当于 $+x-(a-b)=+(b-a)+x$。因此都相当于给每个石头分配或+或-，目标在于找到总和最靠近总重量一半的划分方式。

转换为 01 背包问题，即背包容量为 $\lfloor sum / 2\rfloor$，目前为取出最大价值。

**详情**：[【宫水三叶の相信科学系列】详解为何能转换为背包问题](https://leetcode.cn/problems/last-stone-weight-ii/solutions/818362/gong-shui-san-xie-xiang-jie-wei-he-neng-jgxik)

## 代码
```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        n = len(stones)
        s = sum(stones)
        c = s // 2

        dp = [0] * (c+1)
        for i, stone in enumerate(stones):
            for j in range(c, stone-1, -1):
                dp[j] = max(dp[j], dp[j-stone]+stone)
        return s - 2 * dp[c]
```
