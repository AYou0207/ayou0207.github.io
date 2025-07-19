---
title: 二进制链表转整数
date: 2025-07-19 19:00:00 +0800
categories: [Leetcode, LinkedList]
tags: [leetcode, linked-list]
author: ayou
description: 统计链表中极值节点之间距离的最大与最小距离。遍历并统计。
comments: true
---

## 原题
[1290. 二进制链表转整数](https://leetcode.cn/problems/convert-binary-number-in-a-linked-list-to-integer/description/)

## 题解
**详情**：[遍历链表](https://leetcode.cn/problems/convert-binary-number-in-a-linked-list-to-integer/solutions/3723060/bian-li-lian-biao-pythonjavaccgojsrust-b-ykjd)

## 代码
```python
class Solution:
    def getDecimalValue(self, head: ListNode) -> int:
        answer = 0
        while head.next:
            answer = answer * 2 + head.val
            head = head.next
        answer = answer * 2 + head.val
        return answer
```
