---
title: 搜索二维矩阵
date: 2025-06-15 21:50:00 +0800
categories: [Leetcode, Bisearch]
tags: [leetcode, bisearch, medium]
author: ayou
description: 二位排序数组中查找目标值是否存在。二分。
comments: true
---

## 原题
[74. 搜索二维矩阵](https://leetcode.cn/problems/search-a-2d-matrix/description/)

## 题解
**详情**：[两种方法：二分查找/排除法（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/search-a-2d-matrix/solutions/2783931/liang-chong-fang-fa-er-fen-cha-zhao-pai-39d74)

## 代码
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix), len(matrix[0])

        left, right = -1, m
        while left + 1 < right:
            mid = (left + right) // 2
            if matrix[mid][0] == target:
                return True
            if matrix[mid][0] < target:
                left = mid
            else:
                right = mid
        
        select = left
        left, right = -1, n
        while left + 1 < right:
            mid = (left + right) // 2
            if matrix[select][mid] == target:
                return True
            if matrix[select][mid] < target:
                left = mid
            else:
                right = mid
        
        return False
```
