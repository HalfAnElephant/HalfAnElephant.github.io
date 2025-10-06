---
title: "Codeforces Round 1056 (Div. 2) C. The Ancient Wizards' Capes"
description: "给定每个位置能看到的巫师数量，反向推导有多少种巫师披风的左右穿戴方式组合可以生成这些观察结果。"
date: 2025-10-06T17:08:23+08:00
math: true
license:
hidden: false
image: cover.png
comments: true # 评论
draft: false # 草稿
toc: # 是否开启目录
categories:
  - 编程
  - Codeforces
  - 题解
tags:
  - 编程
  - 算法竞赛
  - Codeforces
  - 题解
  - DP
---

# Codeforces Round 1056 (Div. 2) C. The Ancient Wizards' Capes

[题目链接: Codeforces Round 1056 (Div. 2) C. The Ancient Wizards' Capes](https://codeforces.com/contest/2155/problem/C)

## 题目简述

### 题目大意

给定一个整数 $n$，以及一个长度为 $n$ 的数组 $a$。$a_i$ 表示在位置 $i$ 处可见的巫师数量。
一个巫师 $j$ 在位置 $i$ 处可见的条件是：

巫师 $j$ 将斗篷穿在左侧，且 $i \geq j$。
巫师 $j$ 将斗篷穿在右侧，且 $i \leq j$。

巫师 $i$ 在位置 $i$ 处始终可见。
你的任务是计算与数组 $a$ 一致的斗篷排列方式的数量，结果对 676767677 取模。

### 数据范围

$1\leq n\leq 10^5$

$1\leq t \leq 10^4$

$1\leq a_i \leq n$

$\Sigma n \leq 10^5$

## 题目思路

通过寻找递推关系来简化问题。

我们定义 $d_j$ 表示斗篷朝向，若第 $j$ 个巫师斗篷方向朝右则为 $0$，反之则为 $1$。

由此可得 $a_i$ 表达式:

$$
a_i = \Sigma_{j=1}^i d_j + \Sigma_{j=i}^n(1-d_j)
$$

相邻项做差可得：

$$
a_i - a_{i-1} = d_i + d_{i - 1} - 1
$$

变形得到：

$$
d_i = (a_i-a_{i - 1} + 1) - d_{i-1}
$$

由此可知，$d_i$仅由$d_{i-1}$以及$a_i$、$a_{i - 1}$决定。所以可以假定$d_1$进行检验。此时，我们仅需要检查两种可能，即$d_1$为$0$或$1$.进行假设后进行递推，判断$d_i$是否合法。

### 赛后

[tourist](https://codeforces.com/contest/2155/submission/342045184)

```cpp
for (int r = 0; r < 2; r++) {
    vector<int> b(n);
    b[0] = r;
    for (int i = 1; i < n; i++) {
        b[i] = 1 - (b[i - 1] + a[i] - a[i - 1]);
    }
    int mn = *min_element(b.begin(), b.end());
    int mx = *max_element(b.begin(), b.end());
    if (0 <= mn && mx <= 1) {
        int cnt = 1 + accumulate(b.begin() + 1, b.end(), 0);
        if (cnt == a[0]) {
            ans += 1;
        }
    }
```

使用 STL 简化代码。
