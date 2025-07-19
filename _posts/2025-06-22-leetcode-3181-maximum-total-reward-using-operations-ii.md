---
title: 3181. 执行操作可获得的最大总奖励 II
date: 2025-06-22 22:10:00 +0800
categories: [Leetcode, Backpack]
tags: [leetcode, backpack, hard, bitset]
author: ayou
description: 在数组中选取一些数，选取要求满足一定限制，求最终和的最大值。01背包变体 & 位操作优化。
comments: true
math: true
---

## 原题
[3181. 执行操作可获得的最大总奖励 II](https://leetcode.cn/problems/maximum-total-reward-using-operations-ii/description/)

## 题解
**思路**：限制二意味着我们应当从小到大进行数字选取，并且每个数字最多选取一次。同时选取的数字$v$要满足$c\ge v$且$c-v<v$，即 $v\le c< 2v$。转移方程为
$$
\text{dp}(c) = \text{dp}(c) \lor \text{dp}(c-v), \quad v\le c< 2v
$$

**详情**：[bitset/bigint 优化 0-1 背包 + 两数之和优化](https://leetcode.cn/problems/maximum-total-reward-using-operations-ii/solutions/2805413/bitset-you-hua-0-1-bei-bao-by-endlessche-m1xn)

## 代码
```python
class Solution:
    def maxTotalReward(self, rewardValues: List[int]) -> int:
        dp = 1
        for v in rewardValues:
            dp |= (dp & ((1 << v) - 1)) << v
        return dp.bit_length() - 1
```
