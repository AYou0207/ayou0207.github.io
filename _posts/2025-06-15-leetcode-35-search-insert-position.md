---
title: 搜索插入位置
date: 2025-06-15 21:40:00 +0800
categories: [Leetcode, Bisearch]
tags: [leetcode, bisearch, base]
author: ayou
description: 排序数组中找到目标值待插入的位置。二分。
comments: true
---

## 原题
[35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/description/)

## 题解
**思路**：二分。实现时，要注意**循环不变量** 性质的保持。

**详情**：[二分查找总是写不对？一个视频讲透！（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/search-insert-position/solutions/2023391/er-fen-cha-zhao-zong-shi-xie-bu-dui-yi-g-nq23)

## 代码
```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = -1, len(nums)
        while left + 1 < right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid
            else:
                right = mid
        return right
```
