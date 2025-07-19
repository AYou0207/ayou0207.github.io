---
title: 33. 搜索旋转排序数组
date: 2025-06-15 23:20:00 +0800
categories: [Leetcode, Bisearch]
tags: [leetcode, bisearch, medium]
author: ayou
description: 旋转排序数组中找到目标值。二分。
comments: true
---

## 原题
[33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/description/)


## 题解
**思路**：二分。复合题，基础题为[153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/description/)。

**详情**：[两种方法：两次二分/一次二分，简洁写法！（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/search-in-rotated-sorted-array/solutions/1987503/by-endlesscheng-auuh)

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
    
    def search(self, nums: List[int], target: int) -> int:
        i = self.find_min(nums)
        if target > nums[-1]:
            return self.lower_bound(nums, -1, i, target)
        return self.lower_bound(nums, i-1, len(nums), target)
    
    def lower_bound(self, nums: list[int], left: int, right: int, target: int) -> int:
        while left + 1 < right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            if nums[mid] < target:
                left = mid
            else:
                right = mid
        return -1
```
