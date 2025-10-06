---
title: "Codeforces Round 1056 (Div. 2) B. Abraham's Great Escape"
description: "在 n x n 的迷宫中设计箭头的方向，使得恰好有 k 个格子是“可逃脱的起始点”。"
date: 2025-10-06T12:53:51+08:00
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
  - 模拟
---

# Codeforces Round 1056 (Div. 2) B. Abraham's Great Escape

[题目链接: Codeforces Round 1056 (Div. 2) B. Abraham's Great Escape](https://codeforces.com/contest/2155/problem/B)

## 题目简述

### 题目大意

在 $n\times n$ 的迷宫中设计箭头的方向，使得恰好有 $k$ 个格子是“可逃脱的起始点”。

### 数据范围

$1\leq t\leq 1000$

$2\leq n \leq 100,\ 1 \leq k \leq n^2,\ \Sigma n^2 \leq 10^5$

## 题目思路

首先判断无法设计的情况。从样例中可以才测出，当且仅当 `k == n * n - 1` 时迷宫无法被设计，其余所有情况均可设计。

然后构思如何设计。总体思路为，先将所有格子中的方向设为统一方向，即所有格子均为可逃脱的起始点，然后再填入一定数量的无法逃出的方向，以使迷宫满足题意。

赛事思路主要是构造两两冲突，即`[R][L]`之类，以此填充迷宫。剩下如果不够则用上下的`[U]`和`[D]`来构造。此方法构造理论上可行，但实际编写时细节较难处理，多次提交均错误。

### 赛后

赛后观察其他选手代码，发现思路基本接近。例如[tourist](https://codeforces.com/profile/tourist)的[代码](https://codeforces.com/contest/2155/submission/342041165)，先提充最顶层，使得最顶层无法逃出，接下来仅需向下填充网格，若填充`[U]`则无法逃出，若填充`[D]`则可以逃出。具体代码为：

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        if (k > 0) {
          k -= 1;
          if (i == 0 && j == 0) cout << 'R'; else
          if (i == 0) cout << 'L';
          else cout << 'U';
        } else {
            cout << 'D';
        }
      }
      cout << '\n';
    }
```

代码中比较巧妙的是，未使用额外的数组来储存信息，直接按照逻辑输出迷宫，便于节省空间和时间消耗。
