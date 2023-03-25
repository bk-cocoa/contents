---
title: ABC282 E - Choose Two and Eat One
date: 2022-12-17
draft: False
summary: 最大全域木に落とし込みたかった
tags: [ABC,ABC282,E,500点,ボール,グラフ,最小全域木,最大全域木,クラスカル法,プリム法]
katex: math
---
# 問題
[ABC282 E - Choose Two and Eat One](https://atcoder.jp/contests/abc282/tasks/abc282_e)

# お気持ち
* ボールがN個あるじゃん？
* 1回の操作でボール2個取って、1個消して、1個戻すじゃん？
* 操作の回数はN-1回じゃん？
* 木っぽくね？
* この辺から最大全域木までエスパーを受信したかった…
* このエスパーまで受信できたら、後は割と簡単な問題だったのでは…うーむ、悔しい…
* 辺の重みを正の値にすると最小全域木、-1倍してあげると最大全域木で取れるね
* $x^y+y^x$あたりもpowで叩いたら余裕で通ったっぽい…


## プリム法
* 最小全域木を求めるやつ
* heapq使うよ
* 適当な頂点1個決めて、その頂点から生えてる辺を全部heapに突っ込む
* 一番小さい辺と、その先に有る頂点を確定させて、その辺の先にある頂点から生えてる辺も全部heapに突っ込む
* 後は全頂点が確定するまで木を大きく育てる
    * ダイクストラっぽい
    * こっちのほうが若干効率良いらしい

## クラスカル法
* UnionFind使うよ
* 辺をコスト順に並べて小さい方から順に見ていく
* 見てる辺を確定させてた時に閉路ができる？（＝辺の両端は同一集合？）
    * Yes→採用しちゃダメだよ
    * No→この辺採用！！！
* こっちのほうが若干効率悪いっぽい


# ソースコード
```python:E.py
# UnionFind省略

N, M = map(int, input().split())
A_L = list(map(int, input().split()))

edge_L = []

for a in range(N - 1):
    for b in range(a + 1, N):
        x = A_L[a]
        y = A_L[b]
        score = pow(pow(x, y, M) + pow(y, x, M), 1, M)
        edge_L.append((-score, a, b))

edge_L.sort()
uf = UnionFind(N)
ans = 0

for score, a, b in edge_L:
    if not uf.same(a, b):
        uf.union(a, b)
        ans += -score

print(ans)

```