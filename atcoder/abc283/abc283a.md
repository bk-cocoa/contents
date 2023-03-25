---
title: ABC283 A - Power
date: 2022-12-24
draft: False
summary: 計算するだけ
tags: [ABC,ABC283,A,100点,計算,本番AC]
katex: math
---
# 問題
[ABC283 A - Power](https://atcoder.jp/contests/abc283/tasks/abc283_a)
# お気持ち
* AのB乗を出力してね！終わり！
    * Aはこのくらいの難易度でいいんだよ！！！嬉しい！！！
* 本番で一瞬「えっとpow…」とか考えたけど上限9までだったので愚直に書いてあげてよかった
* POWで引数2つならmod取らないの知らなかった
    * pow(A,B,1)とかしてあわあわしてた
    * pow(A,B)でよかった

# ソースコード1
```python:A.py
A, B = map(int, input().split())
print(pow(A, B))
```

# ソースコード2
```python:A.py
A, B = map(int, input().split())
print(A ** B)
```