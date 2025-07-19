---
title: 分隔链表
date: 2025-07-19 19:30:00 +0800
categories: [Leetcode, LinkedList]
tags: [leetcode, linked-list]
author: ayou
description: 将链表分割为 k 个等分的部分。数学+链表遍历。
comments: true
---

## 原题
[725. 分隔链表](https://leetcode.cn/problems/split-linked-list-in-parts/)

## 题解
**详情**：[原地做法，O(1) 空间](https://leetcode.cn/problems/merge-nodes-in-between-zeros/solutions/1278727/jian-ji-xie-fa-by-endlesscheng-c4gf)

## 代码
```python
class Solution:
    def splitListToParts(self, head: Optional[ListNode], k: int) -> List[Optional[ListNode]]:
        n = 0
        node = head
        while node:
            n += 1
            node = node.next
        
        quotient, remainder = divmod(n, k)

        answer = [None for _ in range(k)]
        i, current = 0, head
        while i < k and current:
            answer[i] = current
            part_size = quotient + (1 if i < remainder else 0)
            for _ in range(part_size - 1):
                current = current.next
            current.next, current = None, current.next
            i += 1
        return answer
```
