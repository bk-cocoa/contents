---
title: ABC285 C - abc285_brutmhyhiizp
date: 2023-01-15
draft: false
summary: n進数変換するだけ
tags: [ABC,ABC285,C,300点,26進数,n進数]
katex: math
---
# 問題
[ABC285 CC - abc285_brutmhyhiizp](https://atcoder.jp/contests/abc285/tasks/abc285_c)

# お気持ち
* 26進数を0進数に置換するイメージで。
* A=1,B=2,C=3...Z=26の26進数を10進数に直そうね！


# ソースコード
```python:C.py
S = input()

ans = 0
for i, s in enumerate(S[::-1]):
    ans += 26 ** i * (ord(s) - 64)
print(ans)
```