---
title: 数组中的第K个最大元素
date: 2025-06-21 02:20:00 +0800
categories: [Leetcode, Quicksort]
tags: [leetcode, quicksort, three-way, medium]
author: ayou
description: 求数组内的第 K 大数字。三路快排变种。
comments: true
---

## 原题
[215. 数组中的第K个最大元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/)

## 题解
**详情**：[三路快排变种](https://leetcode.cn/problems/kth-largest-element-in-an-array/solutions/3704933/san-lu-kuai-pai-bian-chong-by-wrran-9ehu)

## 代码
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:

        def partition(left: int, right: int) -> tuple[int, int]:
            pivot = nums[random.randint(left, right)]
            
            index = left
            while index <= right:
                while index <= right and nums[index] > pivot:
                    nums[index], nums[right] = nums[right], nums[index]
                    right -= 1
                if nums[index] < pivot:
                    nums[index], nums[left] = nums[left], nums[index]
                    left += 1
                index += 1
            return left - 1, right


        def split(left: int, right: int, k: int) -> int:
            n_less, n_equal = partition(left, right)
            if n_less < k <= n_equal:
                return nums[n_equal]
            if n_less >= k:
                return split(left, n_less, k)
            return split(n_equal + 1, right, k)

        n = len(nums)
        return split(0, n-1, n-k)
```
