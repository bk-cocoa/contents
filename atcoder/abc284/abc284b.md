---
title: ABC284 B - Multi Test Cases
date: 2023-01-07
draft: false
summary: 奇数数えるだけ
tags: [ABC,ABC284,B,200点,全探索,本番AC]
katex: math
---
# 問題
[ABC284 B - Multi Test Cases](https://atcoder.jp/contests/abc284/tasks/abc284_b)

# お気持ち
* 多分T個のテストケースについて回答するのが本質っぽかったっぽい？
    * AtCoderでは少数派っぽい感じなので…？低diffに導入したかった…のかな…？
* $A_i$を全部見ていって、奇数を数えて出力！
* T回繰り返せば終わり！

# ソースコード
```python:B.py
T = int(input())


def odd_cnt(l):
    ans = 0
    for num in l:
        ans += num % 2 == 1
    return ans


for i in range(T):
    N = int(input())
    A_L = list(map(int, input().split()))
    ans = 0

    print(odd_cnt(A_L))
```