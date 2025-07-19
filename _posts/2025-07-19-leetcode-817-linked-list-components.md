---
title: 817. 链表组件
date: 2025-07-19 19:40:00 +0800
categories: [Leetcode, LinkedList]
tags: [leetcode, linked-list]
author: ayou
description: 计算链表组件个数。“组件”概念理解+链表遍历。
comments: true
---

## 原题
[817. 链表组件](https://leetcode.cn/problems/linked-list-components/description/)

## 题解
**详情**：[简单标志位遍历](https://leetcode.cn/problems/linked-list-components/solutions/2916297/jian-dan-biao-zhi-wei-bian-li-by-zhi-ma-hh3ax)

## 代码
```python
class Solution:
    def numComponents(self, head: Optional[ListNode], nums: List[int]) -> int:
        nums = set(nums)
        in_set = False
        answer = 0
        while head:
            if head.val not in nums:
                in_set = False
            elif not in_set:
                in_set = True
                answer += 1
            head = head.next
        return answer
```
