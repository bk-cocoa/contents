---
title: ABC285 A - Edge Checker 2
date: 2023-01-15
draft: false
summary: 二分木のやつ
tags: [ABC,ABC285,A,100点,二分木,本番AC]
katex: math
---
# 問題
[ABC285 A - Edge Checker 2](https://atcoder.jp/contests/abc285/tasks/abc285_a)
# お気持ち
* 時間かけて全部手打ち`[[1],[2,3],[4,5],[6,7],[8,9],[10,11]...]`でもいいけど…
* `a*2==b or a*2+1==b`で終わり！
    * もっと短くすると`b//2==a`で終わり！
# ソースコード
```python:A.py
a, b = map(int, input().split())
if b // 2 == a:
    print('Yes')
else:
    print('No')　
```