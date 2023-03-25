---
title: ABC283 B - First Query Problem
date: 2022-12-24
draft: False
summary: クエリ処理するだけ
tags: [ABC,ABC283,B,200点,クエリ,本番AC]
katex: math
---
# 問題
[ABC282 B - First Query Problem](https://atcoder.jp/contests/abc283/tasks/abc283_b)

# お気持ち
* 一点更新で、一点出力…えっ、セグ…いやこれ配列でいいじゃないですかやだー
    * Bの難易度はこれくらいでいいんですよ！！！嬉しい！！！
* A_Lを直で更新してあげたら良いね

# ソースコード
```python:B.py
N = int(input())
A_L = list(map(int, input().split()))

Q = int(input())
for i in range(Q):
    q_type, *query = map(int, input().split())

    if q_type == 1:
        k, x = query
        A_L[k - 1] = x
    else:
        k = query[0]
        print(A_L[k - 1])
```