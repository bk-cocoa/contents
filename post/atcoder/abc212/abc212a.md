---
title: ABC212 A - Alloy
date: 2021-07-31
draft: false
summary: 文字列作るだけ
tags: [ABC,ABC282,A,100点,文字列,本番AC]
katex: math
---
# 問題
[ABC282 A - Generalized ABC](https://atcoder.jp/contests/abc282/tasks/abc282_a)
# お気持ち
* 全体の文字列`ABCDEFGHIJKLMNOPQRSTUVWXYZ`を作って
* スライスでほしい部分だけ切り取って
* 終わり！

# 小ネタ
* 全体の文字列を作る部分
    * ループで作る
        * `chr(ord('A')) + i`
    * 文字列手打ち
        * `S = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"`
    * ライブラリから引っ張ってくる
        * `string.ascii_uppercase`

# ソースコード
```python:A.py
S = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

K = int(input())
print(S[:K])
```