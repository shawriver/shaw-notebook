---
title: 完全二叉树
published: 2026-09-06
description: 完全二叉树的定义、性质，以及为什么它适合用数组存储。
tags: ["数据结构", "二叉树"]
category: 数据结构
book: 数据结构
order: 1
draft: false
---

## 一句话定义

除最后一层外，每一层都被节点填满；最后一层的节点全部靠左连续排列。这样的二叉树叫完全二叉树。

关键在"靠左连续"这四个字。最后一层可以不满，但中间不能空出位置。

## 和满二叉树的区别

满二叉树是每一层都填满，节点数刚好是 `2^h - 1`。满二叉树一定是完全二叉树，反过来不成立。

## 几条常用性质

设节点总数为 `n`：

- 高度是 `floor(log2(n)) + 1`
- 叶子节点从下标 `floor(n/2) + 1` 开始（下标从 1 算起）
- 只有最后一个非叶子节点可能只有左孩子，没有右孩子

## 为什么能用数组存

因为节点位置连续，不会出现空洞，所以下标可以直接算出父子关系。下标从 1 开始时：

```c
// 节点 i 的左孩子、右孩子、父节点
left   = 2 * i;
right  = 2 * i + 1;
parent = i / 2;
```

下标从 0 开始时：

```c
left   = 2 * i + 1;
right  = 2 * i + 2;
parent = (i - 1) / 2;
```

不用存指针，省空间，访问也快。堆（优先队列）就是靠这个性质实现的。

## 判断是不是完全二叉树

层序遍历，遇到空节点就停止往队列里加，然后检查队列里剩下的是否全为空。如果后面还出现了非空节点，说明中间有空洞，不是完全二叉树。

```c
bool isComplete(Node *root) {
    if (!root) return true;

    Node *queue[MAXN];
    int head = 0, tail = 0;
    queue[tail++] = root;
    bool metNull = false;

    while (head < tail) {
        Node *cur = queue[head++];
        if (cur == NULL) {
            metNull = true;      // 记录已经遇到过空位
        } else {
            if (metNull) return false;   // 空位后面又出现节点，有空洞
            queue[tail++] = cur->left;
            queue[tail++] = cur->right;
        }
    }
    return true;
}
```

## 容易踩的点

- 最后一层节点数可以是 1 到 `2^(h-1)` 之间任意值，但必须从左往右连着放
- "只缺右孩子"是允许的，"只缺左孩子"不允许
- 数组存储只对完全二叉树划算，普通二叉树用数组会浪费很多空位
