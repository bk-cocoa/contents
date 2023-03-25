---
title: ABC282 B - Let's Get a Perfect Score
date: 2022-12-17
draft: false
summary: 全探索
tags: [ABC,ABC282,B,200点,全探索,本番AC]
katex: math
---
# 問題
[ABC282 B - Let's Get a Perfect Score](https://atcoder.jp/contests/abc282/tasks/abc282_b)

# お気持ち
* 参加者の再大人数は$30$人と少ないね
* 全ペア考えたとしても$\frac{30 \times 29}{2} = 435$組で余裕
* 全ペアについてM問ずつ確認したとしても、$435 \times 30 = 13050$回のチェックで余裕
* 全ペア確認できるなら全ペア確認しちゃお
* 判定部分の実装に関しては割と宗派が分かれそう
    * 黒ココアさんは`for else`が良いかもしれない。
    * フラグ持たせたりとかするのも
    * 関数作ったり…Bでそこまでするのは手間かなぁ…？無しでは無し…？
    * 入力の時に2進数変換しておいて`or`で取るとスマート…？

# ソースコード
```python:B.py
N, M = map(int, input().split())
L = []
for i in range(N):
    S = input()
    L.append(S)

ans = 0

for i in range(N-1):
    for j in range(i+1, N):
        for question in range(M):
            if L[i][question] == 'x' and L[j][question] == 'x':
                break
        else:
            ans += 1

print(ans)

```