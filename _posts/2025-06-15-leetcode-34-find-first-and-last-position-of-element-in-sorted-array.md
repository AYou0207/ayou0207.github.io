---
title: 在排序数组中查找元素的第一个和最后一个位置
date: 2025-06-15 21:55:00 +0800
categories: [Leetcode, Bisearch]
tags: [leetcode, bisearch, medium]
author: ayou
description: 排序数组中找到目标值的开始与结束位置。二分。
comments: true
---

## 原题
[34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

## 题解
**思路**：二分。实现时，可以通过两次二分找到开始与结束位置；首次以条件 `nums[mid] < target` 找到开始位置；接着以条件 `nums[mid] <= target` 找到结束位置。

**详情**：[【视频讲解】二分查找总是写不对？三种写法，一个视频讲透！（Python/Java/C++/C/Go/JS）](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/solutions/1980196/er-fen-cha-zhao-zong-shi-xie-bu-dui-yi-g-t9l9)

## 代码
```python
class Solution:
    def searchRange(self, nums: list[int], target: int) -> list[int]:
        n = len(nums)
        
        # find the first item < target
        left, right = -1, n
        while left + 1 < right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid
            else:
                right = mid
        
        if right == n or nums[right] != target:
            return [-1, -1]
        
        # find the first item > target
        start = right
        left, right = right, n
        while left + 1 < right:
            mid = (left + right) // 2
            if nums[mid] <= target:
                left = mid
            else:
                right = mid
        
        end = right - 1
        return [start, end]
```
