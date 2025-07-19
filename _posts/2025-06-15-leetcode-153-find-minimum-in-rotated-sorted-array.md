---
title: 153. 寻找旋转排序数组中的最小值
date: 2025-06-15 23:15:00 +0800
categories: [Leetcode, Bisearch]
tags: [leetcode, bisearch, medium]
author: ayou
description: 旋转排序数组中找到最小值。二分。
comments: true
---

## 原题
[153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/description/)

## 题解
**思路**：二分。关键点在于：比较 `mid` 与 `nums[-1]`，并确定如何更新 `left` & `right`。

**详情**：[和最后一个数比大小，简洁二分（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/solutions/1987499/by-endlesscheng-owgd)

## 代码
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left, right = -1, len(nums)
        while left + 1 < right:
            mid = (left + right) // 2
            if nums[mid] > nums[-1]:
                left = mid
            else:
                right = mid
        return nums[right]
```
