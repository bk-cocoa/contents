---
title: ABC282 C - String Delimiter
date: 2022-12-17
draft: false
summary: 先頭から見ていく文字列置換
tags: [ABC,ABC282,C,300点,線形時間,文字列,本番AC]
katex: math
---
# 問題
[ABC282 C - String Delimiter](https://atcoder.jp/contests/abc282/tasks/abc282_c)

# お気持ち
* 先頭から順に見て、文字がダブルコーテーションで*括られている*か*括られていない*かを判断していけば良さそう
* フラグの切り替え忘れずに！
* 文字列は最後に一括でjoinしないと死ぬ(Python)

# ソースコード
```python:C.py
N = int(input())
S = input()
ans_L = []
kukurare_flg = False

for s in S:
    if s == ','and 
        if not kukurare_flg:
            s = '.'
    elif s == '"':
        if kukurare_flg:
            kukurare_flg = False
        else:
            kukurare_flg = True
    ans_L.append(s)

print(''.join(ans_L))
```