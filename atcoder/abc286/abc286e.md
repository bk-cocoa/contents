---
title: ABC286 E - Souvenir
date: 2023-01-21
draft: False
summary: ワーシャルフロイドに要素を一つ
tags: [ABC,ABC285,E,500点,ワーシャルフロイド,グラフ]
katex: math
---
# 問題
[ABC286 E - Souvenir](https://atcoder.jp/contests/abc286/tasks/abc286_e)

# お気持ち
* 制約の$N \leq 300$から、$O(N^3)$が通る！
* クエリ形式でいろんな都市間の経路を問われる！
    * ワーシャルフロイドで全都市間のルートを前処理してたら都合が良いですね！
* あとはワーシャルフロイドの更新部分に、お土産の価値の総和も追加してあげたら良し

# ソースコード
```python:E.py
N = int(input())
A_L = list(map(int, input().split()))

inf = 10 ** 18
dist = [[inf for i in range(N)] for j in range(N)]
val = [[0 for i in range(N)] for j in range(N)]

for i in range(N):
    S = input()
    for j, c in enumerate(S):
        if c == 'Y':
            dist[i][j] = 1
            val[i][j] = A_L[i] + A_L[j]

for i in range(N):
    dist[i][i] = 0

for m in range(N):
    for s in range(N):
        for g in range(N):

            if dist[s][g] > dist[s][m] + dist[m][g]:
                dist[s][g] = dist[s][m] + dist[m][g]
                val[s][g] = val[s][m] + val[m][g] - A_L[m]
            elif dist[s][g] == dist[s][m] + dist[m][g]:
                val[s][g] = max(val[s][g], val[s][m] + val[m][g] - A_L[m])

Q = int(input())
for i in range(Q):
    U, V = map(int, input().split())
    U -= 1
    V -= 1

    if dist[U][V] == inf:
        print('Impossible')
    else:
        print(dist[U][V], val[U][V])

```