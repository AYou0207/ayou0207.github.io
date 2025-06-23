---
title: k 镜像数字的和
date: 2025-06-23 21:45:00 +0800
categories: [Leetcode, Palindrome]
tags: [leetcode, palindrome, template]
author: ayou
description: 找出 k 进制下的回文数，枚举+回文数判断即可。
comments: true
---

## 原题
[2081. k 镜像数字的和](https://leetcode.cn/problems/sum-of-k-mirror-numbers/)

## 题解
**详情**：[【模板】枚举回文数](https://leetcode.cn/problems/sum-of-k-mirror-numbers/solutions/1113431/da-biao-zuo-fa-by-endlesscheng-7ojf)

## 代码
```python
MAX_N = 30
answer = [[] for _ in range(30)]

def is_k_palindrome(x: int, k: int) -> bool:
    if x % k == 0:
        return False
    rev = 0
    while rev < x // k:
        rev = rev * k + x % k
        x //= k
    return rev == x or rev == x // k


def do_palindrome(x: int) -> bool:
    done = True
    for k in range(2, 10):
        if len(answer[k]) < MAX_N and is_k_palindrome(x, k):
            answer[k].append(x)
        if len(answer[k]) < MAX_N:
            done = False
    if not done:
        return False
    for k in range(2, 10):
        answer[k] = list(accumulate(answer[k]))
    return True


def init():
    base = 1
    while True:
        # 生成奇数长度回文数，例如 base = 10，生成的范围是 101 ~ 999
        for i in range(base, base * 10):
            s = str(i)
            x = int(s + s[::-1][1:])
            if do_palindrome(x):
                return
        # 生成偶数长度回文数，例如 base = 10，生成的范围是 1001 ~ 9999
        for i in range(base, base * 10):
            s = str(i)
            x = int(s + s[::-1])
            if do_palindrome(x):
                return
        
        base *= 10

init()

class Solution:
    def kMirror(self, k: int, n: int) -> int:
        return answer[k][n-1]
```
