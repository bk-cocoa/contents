---
title: ABC286 A - Range Swap
date: 2023-01-21
draft: false
summary: 配列ちぎるやつ
tags: [ABC,ABC286,A,100点,配列操作,スライス]
katex: math
---
# 問題
[ABC286  A - Range Swap](https://atcoder.jp/contests/abc286/tasks/abc286_a)
# お気持ち
* A問題で時間取られたのもったいなかったなー。
    * スライスで添字ガチャしてしまった…むーん。
    * 必要なところだけ切って並び替えたら終わり！
# ソースコード
```python:A.py
N, P, Q, R, S = map(int, input().split())
L = list(map(int, input().split()))

print(*L[:P - 1] + L[R - 1:S] + L[Q:R - 1] + L[P - 1:Q] + L[S:])
```