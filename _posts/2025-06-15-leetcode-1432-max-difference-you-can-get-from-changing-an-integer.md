---
title: 改变一个整数能得到的最大差值
date: 2025-06-15 14:00:00 +0800
categories: [Leetcode, Greedy]
tags: [leetcode, greedy, easy]
author: ayou
description: 将字符串中的某个数字全部替换，但不可出现前导0，求最大差值。贪心可解。
comments: true
---

## 原题
[1432. 改变一个整数能得到的最大差值](https://leetcode.cn/problems/max-difference-you-can-get-from-changing-an-integer/description/)

## 题解
**思路**：贪心

**详情**：[贪心 O(num) 做法（Python/Java/C++/C/Go/JS/Rust）](https://leetcode.cn/problems/max-difference-you-can-get-from-changing-an-integer/solutions/3690149/tan-xin-pythonjavaccgojsrust-by-endlessc-k8iw)

与 1432 题相近，但该题不允许有前导0；因此在进行最小值计算时，注意特殊情形的区分。

## 代码
```python
class Solution:
    def maxDiff(self, num: int) -> int:
        s = str(num)

        mx = num
        for ch in s:
            if ch != '9':
                mx = int(s.replace(ch, '9'))
                break
        
        mn = num
        if s[0] != '1':
            mn = int(s.replace(s[0], '1'))
        else:
            for ch in s:
                if ch > '1':
                    mn = int(s.replace(ch, '0'))
                    break
        
        return mx - mn
```