---
title: ABC284 C - Count Connected Components
date: 2023-01-07
draft: false
summary: グループ数数えてるだけ
tags: [ABC,ABC284,C,300点,UnionFind,本番AC]
katex: math
---
# 問題
[ABC284 C - Count Connected Components](https://atcoder.jp/contests/abc284/tasks/abc284_c)

# お気持ち
* UnionFindでunionしていって、
* rootの数数えて、終わり！

# ソースコード
```python:C.py
N, M = map(int, input().split())
uf = UnionFind(N)
for i in range(M):
    u, v = map(int, input().split())
    u -= 1
    v -= 1
    uf.union(u, v)
print(uf.group_count())
```