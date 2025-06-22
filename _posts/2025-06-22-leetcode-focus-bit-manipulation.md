---
title: 【专题】位操作
date: 2025-06-22 15:00:00 +0800
categories: [Leetcode, Focus]
tags: [leetcode, bit-manipulation]
author: ayou
description: 常见的位操作技巧。
math: true
comments: true
---

## 集合与元素

|术语|集合|位运算|
|:--|:--|:-----|
|空集|$\emptyset$|`0`|
|单元素集合|$\{i\}$|`1 << i`|
|全集|$U = \{0, 1, \cdots, n-1\}$|`(1 << n) - 1`|
|补集|$U \backslash S$|`((1 << n) - 1) ^ s`|
|属于|$i\in S$|`(s >> i) & 1 = 1`|
|不属于|$i\not\in S$|`(s >> i) & 1 = 0`|
|添加元素|$S\cup \{i\}$|`s | (1 << i)`|
|删除元素|$S \backslash \{i\}$|`s & ~(1 << i)`|
|删除集合中的元素|$S \backslash \{i\}, i \in S$|`s ^ (1 << i)`|


特别地，常用的**只包含最小元素的子集**（也称为 lowbit）的运算为 `s & -s`；示例如下：
```python
        s = 101_100
       ~s = 010_011
-s = ~s+1 = 010_100
   s & -s = 000_100
```
{: file="LOWBIT: s & -s" }

特别地，常用的**删除最小元素**的运算为 `s & (s-1)`；示例如下：
```python
      s = 101_100
    s-1 = 101_011
s&(s-1) = 101_000
```
{: file="REMOVE LOWBIT: s & (s-1)" }

以下是与集合相关的常见操作，这些函数的时间复杂度都是 $O(1)$。

|术语|Python|
|:--|:-----|
|集合大小｜`s.bit_count()`|
|二进制长度｜`s.bit_length()`|
|集合最大元素｜`s.bit_length()-1`|
|集合最小元素｜`(s & -s).bit_length()-1`|

## 遍历集合
### 范围枚举
当知道元素范围在 $[0, n-1]$之间时，我们可以枚举范围，判断是否在集合中即可。
```python
for i in range(n):
    if (s >> i) & 1:
        ...
```

### 最小元素枚举
直接遍历集合 `s` 中的元素：不断取出集合中的最小元素，直到集合为空。
```python
while s:
    lowbit = s & -s
    s ^= lowbit
    item = lowbit.bit_length() - 1
```

## 枚举集合
### 枚举全集
已知元素范围为 $[0, n-1]$，从空集 $\emptyset$ 逐步枚举到全集 $U$：
```python
for s in range(1 << n):
    ...
```

### 枚举非空子集
直接遍历集合 `s` 的非空子集：不断取出集合中的最小元素，注意跳过空集。
```python
while s:
    ...
    s = s & (s-1)
```

### 枚举所有子集
直接遍历集合 `s` 的所有子集：不断取出集合中的最小元素，直至遇到空集。
```python
while True:
    ...
    if s == 0:
        break
    s = s & (s-1)
```

### 枚举超集
枚举集合 `t` 的超集：通过或运算保证枚举的集合 `s` 一定包含集合 `t` 中的所有元素。
```python
s = t
while s < (1 << n):
    ...
    s = (s+1) | t
```

### 枚举大小为K的集合
枚举集合元素个数为$K$的集合，该技巧称为 **Gosper's Hack**。
```python
s = 1 << k - 1
while s < (1 << n):
    ...
    lowbit = s & -s
    high = s + lowbit
    low = (s ^ high) // lowbit >> 2
    s = high | low
```

#### 讲解
[Gosper's Hack - 灵茶山艾府の讲解](https://www.bilibili.com/video/BV1na41137jv/)

[Gosper's Hack - 推导](https://zhuanlan.zhihu.com/p/360512296)

> 第二个讲解中，代码是错误的；但思路正确。注意甄别。
{: .prompt-warning}

构造思路如下：
1. 找到从右往左第一个`01`串，转换为`10`
2. 将上述`01`串后续的所有`1`放置到最右侧

示意如下：
```
      s = 101_100
   high = 110_...
    low = ..._001
```

高位 `high` 构造思路为 `s + lowbit`，由二进制进位可知，该操作的正确性：
```python
       s = 101_100
  lowbit = 000_100
s+lowbit = 110_000
```

低位 `low` 构造思路 `(s ^ high) // lowbit >> 2` 为：
1. 排除所有不含在 `high` 的元素集合
2. 将它们放置到最右端，可以通过去除后缀 `0` 实现

**第一步**可以通过 `s ^ high` 来得到，但应当注意其最左端的两个`1`应当在最后时刻排除掉（他们分别对应`01`串转换前后）；
**第二步**可以通过除法 `... // lowbit` 来得到。


## 参考
[分享｜从集合论到位运算，常见位运算技巧分类总结！](https://leetcode.cn/discuss/post/3571304/cong-ji-he-lun-dao-wei-yun-suan-chang-ji-enve/)
[Binary Fundamentals](https://terathon.com/binary_fund.pdf)
