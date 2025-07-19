---
title: 2566. 替换一个数字后的最大差值
date: 2025-06-15 12:30:00 +0800
categories: [Leetcode, Greedy]
tags: [leetcode, greedy, easy]
author: ayou
description: 将字符串中的某个数字全部替换，求最大差值。贪心可解。
comments: true
---

## 原题
[2566. 替换一个数字后的最大差值](https://leetcode.cn/problems/maximum-difference-by-remapping-a-digit/)

## 题解
**思路**：贪心

**详情**：[贪心 O(n) 做法（Python/Java/C++/Go）](https://leetcode.cn/problems/maximum-difference-by-remapping-a-digit/solutions/2119447/mei-ju-by-endlesscheng-slfa)

## 代码
```python
class Solution:
    def minMaxDifference(self, num: int) -> int:
        s = str(num)
        mx = num
        for c in s:
            if c != '9':
                mx = int(s.replace(c, '9'))
                break
        mn = int(s.replace(s[0], '0'))
        return mx - mn
```