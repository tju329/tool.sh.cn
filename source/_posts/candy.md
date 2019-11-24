---
title: 糖果问题
date: 2019-11-24 11:10:57
categories: 
- 算法
tags:
- 动态规划
- python
- 策略
- 游戏

---

## 问题描述

幼儿园老师在桌上放了一堆糖果M颗。他让小朋友两两一组做游戏，比如小明和小华一组，他们两人轮流（小明先拿）从桌上拿苹果，每次拿的糖果必须是整数：n1, n2, n3, ..., nk中的一个，谁能拿到最后一颗糖果就算胜利。假定小明和小华都能采取最优策略，谁会获胜？另外假定 n1, n2, n3, ..., nk 中一定含有数字1。

一些限制条件：1 <= M <= 500; 1 <= k <= 50; 1 <= nk <= M;

输入：糖果数 M, k，以及 n1, n2, n3, ..., nk

输出：获胜者（小明或是小华）

## 代码

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

def solve(M, n_list, solutions):
    if M > len(solutions) or M < 0:
        return

    if (M == 0):
        solutions[M] = [0, "输，没能拿最后一个"]
        return
    if (M in n_list):
        solutions[M] = [1, "赢，全部拿走"]
        return
    for k in n_list:
        if (M-k > 0 and solutions[M-k][0] == 0):
            solutions[M] = [1, "赢，拿掉{}个剩余{}个致对手输".format(k, M-k)]
            return

    solutions[M] = [0, "无必赢方案"]
    return


def candy(M, n_list):
    solutions = [0, ""] * (M + 1)  # solutions: 1 - 先玩者赢；0 - 先玩者输；
    for i in range(M + 1):
        solve(i, n_list, solutions)
        print(i, solutions[i][1])

if __name__ == "__main__":
    M = int(input("糖果总数(正整数)："));
    n_list = input("每次拿的糖果数(空格分割，正整数列表：").split(" ");
    n_list = sorted([int(i) for i in set(n_list + [1])]);
    assert all([i > 0 for i in n_list]);
    candy(M, n_list)
```
