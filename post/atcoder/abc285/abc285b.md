---
title: ABC285 B - Longest Uncommon Prefix
date: 2023-01-15
draft: false
summary: 文字列確認するだけ
tags: [ABC,ABC285,B,200点,全探索,本番AC]
katex: math
---
# 問題
[ABC285 B - Longest Uncommon Prefix](https://atcoder.jp/contests/abc285/tasks/abc285_b)

# お気持ち
* 愚直に全探索回してあげてよし！
* 問題文の意味が中々理解しにくいのでサンプル見て手で実験すると良い気がしますね

# ソースコード
```python:B.py
N = int(input())
S = input()

for i in range(1, N):
    ans = 0
    for k in range(N - i):
        if S[k] == S[k + i]:
            break
        else:
            ans += 1
    print(ans)
```