---
title: ABC286 G - Unique Walk
date: 2023-01-21
draft: False
summary: unionfindして数えるだけの黄diff
tags: [ABC,ABC285,G,600点,UnionFind]
katex: math
---
# 問題
[ABC286 G - Unique Walk](https://atcoder.jp/contests/abc286/tasks/abc286_g)

# お気持ち
* 黄diffが！！！G問題が！！！本番AC通せるとは！！！
* ミラクルで通せたの目っっっっっっっっっちゃ嬉しい…！！！
* 制約とかぼんやり見てみる
    * $S$に含まれる辺は1回ずつ通りたい
        * 一筆書きしたい話？
            * [一筆書き](https://ja.wikipedia.org/wiki/%E4%B8%80%E7%AD%86%E6%9B%B8%E3%81%8D)
            * この辺見てみる
            * 全頂点の次数が偶数 or 次数が奇数の頂点が2つの時、一筆書き可能判定ができるっぽい
    * $S$に含まれていない辺は何回通っても良い
    * $G$は連結
        * $S$に関係ない辺で結ばれてる頂点は一緒にして構わないっぽい？
            * SCCとかUnionFindとかの話？
* とりあえずUnionFindで考えてみる
* 一旦辺の一覧を受け取って、
* 部分集合Sも受け取って。
* 部分集合に含まれていない辺を全部結合する
    * ここで同じ根に属する頂点は何回でも行き来可能！
* Sに含まれる辺の場合、辺の両頂点のカウンタを取得して…
    * 次数を数えたいイメージ！
* 最終的に数えた次数リストの、「奇数の数」が0個 or 「奇数の数」が2個の時、一筆書き可能！！！


# ソースコード
```python:E.py
# UnionFind省略

N, M = map(int, input().split())
uf = UnionFind(N)
edge_L = []
for i in range(M):
    u, v = map(int, input().split())
    u -= 1
    v -= 1
    edge_L.append([i + 1, u, v])
K = int(input())
x_s = set(map(int, input().split()))

for i, u, v in edge_L:
    if i not in x_s:
        uf.union(u, v)

deg_L = [0] * N
for i in x_s:
    _, u, v = edge_L[i - 1]
    deg_L[uf.find(u)] ^= 1
    deg_L[uf.find(v)] ^= 1

if deg_L.count(1) in (0, 2):
    print('Yes')
else:
    print('No')
```