---
title: ABC286 D - Money in Hand
date: 2023-01-21
draft: false
summary: グラフに落とし込むと簡単
tags: [ABC,ABC286,D,400点,グラフ,UnionFind]
katex: math
---

# 問題
[ABC286 D - Money in Hand](https://atcoder.jp/contests/abc286/tasks/abc286_d)

# お気持ち
* 雰囲気としてDPっぽい感じのある結局全探索感
* セットで全探索ゴリ押ししてしまった雰囲気が否めず。反省。
* 最外周のループが最大50週
* 真ん中のループが最大$10^4$週
* 内側のループが最大50週
* 合計で$50 \times 50 \times 10^4 = 2.5 \times 10^7$でまぁ間に合ったお話。

# ソースコード
```python:D.py
N, X = map(int, input().split())
wallet_L = []
for i in range(N):
    A, B = map(int, input().split())
    wallet_L.append([A, B])

wallet_s = set()
wallet_s.add(0)

for coin_price, limit_cnt in wallet_L:
    next_s = set()
    next_s.add(0)

    for price in wallet_s:

        for use_cnt in range(limit_cnt + 1):

            add_price = use_cnt * coin_price
            new_price = add_price + price

            if new_price > X:
                break
            next_s.add(new_price)
    wallet_s = next_s

    if X in wallet_s:
        print('Yes')
        exit()

print('No')


```
