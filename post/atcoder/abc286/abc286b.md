---
title: ABC286 B - Cat
date: 2023-01-21
draft: false
summary: にゃーん
tags: [ABC,ABC286,B,200点,文字列操作,置換]
katex: math
---
# 問題
[ABC286 B - Cat](https://atcoder.jp/contests/abc286/tasks/abc286_b)

# お気持ち
* replaceで置換してあげたら瞬殺！

# ソースコード
```python:B.py
N = int(input())
S = input()

print(S.replace('na', 'nya'))
```