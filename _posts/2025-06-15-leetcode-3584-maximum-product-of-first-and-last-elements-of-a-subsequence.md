---
title: 子序列首尾元素的最大乘积
date: 2025-06-15 14:50:00 +0800
categories: [Leetcode]
tags: [leetcode, medium]
author: ayou
description: 求数组中长度为`m`的子序列的首尾元素的最大乘积。枚举右，维护左。
comments: true
---

## 原题
[3584. 子序列首尾元素的最大乘积](https://leetcode.cn/problems/maximum-product-of-first-and-last-elements-of-a-subsequence/description/)

## 题解
**思路**：枚举右，维护左。

**详情**：[脑筋急转弯 + 枚举右维护左（Python/Java/C++/Go）](https://leetcode.cn/problems/maximum-product-of-first-and-last-elements-of-a-subsequence/solutions/3700555/nao-jin-ji-zhuan-wan-mei-ju-you-wei-hu-z-93zo)

## 代码
```python
class Solution:
    def maximumProduct(self, nums: List[int], m: int) -> int:
        answer = -inf
        mx = -inf
        mn = inf
        for i in range(m-1, len(nums)):
            num = nums[i-m+1]
            mn = min(mn, num)
            mx = max(mx, num)
            x = nums[i]
            answer = max(answer, x * mn, x * mx)
        return answer
```
