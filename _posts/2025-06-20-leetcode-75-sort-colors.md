---
title: 75. 颜色分类
date: 2025-06-20 19:30:00 +0800
categories: [Leetcode, Template]
tags: [leetcode, quicksort, three-way, template, base]
author: ayou
description: 荷兰国旗问题。夯实基础-三路快排。
comments: true
---

## 原题
[75. 颜色分类](https://leetcode.cn/problems/sort-colors/description/)

## 题解
**详情**：[颜色分类](https://leetcode.cn/problems/sort-colors/solutions/437968/yan-se-fen-lei-by-leetcode-solution)

## 代码
```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        pivot = 1
        left = 0
        right = len(nums) - 1

        index = left
        while index <= right:
            while nums[index] > pivot and index <= right:
                nums[index], nums[right] = nums[right], nums[index]
                right -= 1
                
            if nums[index] < pivot:
                nums[index], nums[left] = nums[left], nums[index]
                left += 1
            index += 1
```
