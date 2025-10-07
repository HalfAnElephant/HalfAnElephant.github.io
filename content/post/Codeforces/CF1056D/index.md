---
title: "Codeforces Round 1056 (Div. 2) D. Batteries"
description: "通过分组询问找出正常的电池。"
date: 2025-10-06T18:18:00+08:00
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
  - 交互式
---

# Codeforces Round 1056 (Div. 2) D. Batteries

[题目链接: Codeforces Round 1056 (Div. 2) D. Batteries](https://codeforces.com/contest/2155/problem/D)

## 题目简述

### 题目大意

在有限的尝试次数内，通过将电池配对测试手电筒来找到两个工作电池，同时面对一个会动态改变电池好坏状态的裁判器。

### 数据范围

$1\leq t\leq 50$

$2\leq n\leq 40$

$\Sigma n \leq 200$

每个样例尝试次数 $\leq \lfloor \frac{n^2}{a}\rfloor$

## 题目思路

关键在于**会动态调整的交互器**，即若采取较差策略，消耗过多测试机会的话，那么将会动态调整后续安排，将电池安排到策略未包含的地方。

因此我们采取**先小块后大块**的策略，先查询长度为 2 的块内部所有对，然后依次为 3、4……

### 赛后

[补题链接](https://codeforces.com/contest/2155/submission/342375592)
