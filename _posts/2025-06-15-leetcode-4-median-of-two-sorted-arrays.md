---
title: 寻找两个正序数组的中位数
date: 2025-06-15 23:40:00 +0800
categories: [Leetcode, Bisearch]
tags: [leetcode, bisearch, hard]
author: ayou
description: 两个排序数组计算中位数。二分。
comments: true
---

## 原题
[4. 寻找两个正序数组的中位数](https://leetcode.cn/problems/median-of-two-sorted-arrays/description/)


## 题解
**思路**：二分。思维题。在二分中，**循环不变量**为`a[left] <= b[j+1]` & `a[right] > b[j+1]`。

**详情**：[【图解】循序渐进：从双指针到二分（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/median-of-two-sorted-arrays/solutions/2950686/tu-jie-xun-xu-jian-jin-cong-shuang-zhi-z-p2gd)

## 代码
```python
class Solution:
    def findMedianSortedArrays(self, a: List[int], b: List[int]) -> float:
        if len(a) > len(b):
            a, b = b, a
        
        m, n = len(a), len(b)
        left, right = -1, m
        while left + 1 < right:
            mid = (left + right) // 2
            target = (m+n-3) // 2 - mid
            if a[mid] < b[target + 1]:
                left = mid
            else:
                right = mid
        
        i = left
        j = (m+n-3) // 2 - i

        ai = a[i] if i >= 0 else -inf
        bj = b[j] if j >= 0 else -inf
        ai1 = a[i+1] if i+1 < m else inf
        bj1 = b[j+1] if j+1 < n else inf
        mx = max(ai, bj)
        mn = min(ai1, bj1)
        return mx if (m+n) % 2 else (mx+mn) / 2
```
