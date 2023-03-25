---
title: ABC284 A - Sequence of Strings
date: 2023-01-07
draft: false
summary: 逆順にするだけ
tags: [ABC,ABC284,A,100点,配列,逆順,本番AC]
katex: math
---
# 問題
[ABC284 A - Sequence of Strings](https://atcoder.jp/contests/abc284/tasks/abc284_a)
# お気持ち
* 配列に順番に入れていって…
* 逆順に出力したら、はいおわり！

# ソースコード
```python:A.py
N = int(input())
L = []
for i in range(N):
    L.append(input())

for s in L[::-1]:
    print(s)
```