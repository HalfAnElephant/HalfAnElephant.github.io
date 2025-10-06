---
title: 珂朵莉树
description: 有关珂朵莉树的介绍，适用于区间复制、拆分、查找和自定义操作。
date: 2022-08-07T18:02:25+08:00
# slug: abcdafsaf
image: cover.jpg
categories:
  - 编程
  - 数据结构
tags:
  - 数据结构
  - 树
  - 编程
  - 算法竞赛
# weight: 1
---

# 珂朵莉树

**适用于区间复制、拆分、查找和自定义操作**

- 时间复杂度：
  - `set`实现：$O\left(nloglog_2n\right)$
  - `链表`实现：$O\left(n log_2n\right)$

### mutable 的作用：

> `mutable` 的意思是“可变的”，让我们可以在后面的操作中修改 `v` 的值。在 C++ 中，mutable 是为了突破 const 的限制而设置的。被 mutable 修饰的变量（mutable 只能用于修饰类中的非静态数据成员），将永远处于可变的状态，即使在一个 const 函数中。
>
> 这意味着，我们可以直接修改已经插入 `set` 的元素的 `v` 值，而不用将该元素取出后重新加入 `set`。

## 实现：

### 节点保存：

```cpp
struct Node_t
{
    int l, r;
    mutable int v;

    Node_t(const int &il, const int &ir, const int &iv) : l(il), r(ir), v(iv) {}
    inline bool operator<(const Node_t &o) const { return l < 0.l; }
};
set<Node_t> odt;
```

其中，v 是附加数据。

### 分裂区间：

```cpp
set<Node_t>::iterator split(int x)
{
    if (x > n)
    {
        return odt.end();
    }

    auto it = --odt.upper_bound((Node_t){x, 0, 0});
    if (it->l == x)
    {
        return it;
    }

    int l = it->l;
    int r = it->r;
    int v = it->v;

    odt.erase(it);
    odt.insert(Node_t(l, x - 1, v));
    return odt.insert(Node_t(x, r, v)).first;
}
```

将包含点`x`的区间(设为[l, r]),分裂为两个区间[l, r)和[x, r],返回指向**后者**的迭代器。

**任何对于==[l, r]==的区间操作，都可以转换成`set`上对==$[split(l),split(r+1)]$==的操作。**

### 区间赋值：

```cpp
void assign(int l, int r, int v)
{
    auto itr = split(r + 1), itl = split(l);
    odt.erase(itl, itr);
    odt.insert(Node_t(l, r, v));
}
```

### 其余操作套模板：

```cpp
void performance(int l, int r)
{
    auto itr = split(r + 1), itl = split(l);
    for (; itl != itr; ++itl)
    {
        // Perform Operations here
    }
}
```
