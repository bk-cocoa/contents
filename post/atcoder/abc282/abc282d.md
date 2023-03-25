---
title: ABC282 D - Make Bipartite 2
date: 2022-12-17
draft: false
summary: 二部グラフ作ろう2
tags: [ABC,ABC282,D,400点,グラフ,二部グラフ,本番未AC,UnionFind]
katex: math
---

# 問題
[ABC282 D - Make Bipartite 2](https://atcoder.jp/contests/abc282/tasks/abc282_d)

# お気持ち
* やること多くて実装力不足により本番3完で止まった原因問題
* めっちゃ重い…色々勉強になる部分はあった良問、かもしれない…
    * 木は二部グラフ
    * スターグラフは木であり、二部グラフ
    * 二部グラフではないグラフに辺を足して二部グラフになることは無い
    * 閉路のある二部グラフも有る
* まず全頂点連結のグラフの場合で考える
    * 与えられたグラフは二部グラフですか？
        * いいえ→じゃあ何足しても二部グラフにはなれない…
        * はい→白頂点の数 × 黒頂点の数 - 既にある辺の数が追加できる辺 = 追加できる辺の数
* 今回の問題は、連結で有ることが約束されていない=連結じゃないグラフを与えられる場合もある
    * 各連結成分毎に「二部グラフか」の判断を行う
        * 「二部グラフじゃない」連結成分が1つでもあれば二部グラフにはなれない…
    * 「連結な二部グラフ」に、頂点を1つ足すことを考える
        * 連結した二部グラフ内の頂点どれか1つ＋追加した頂点に辺を張っても、それは二部グラフ
            * 追加した頂点は好きな色で塗れば良いからね
    * じゃあ、「連結な二部グラフA」と「連結な二部グラフB」を合わせることを考えてみる
        * Aの白頂点は、Aの黒頂点と繋がっても二部グラフ、継続！
            * Bのどの点と繋がっても、二部グラフ、継続！
                * Bの白黒を切り替えて調整したらいいからね
* ここまで纏めて…
    * 連結成分ごとに分ける
    * それぞれの連結成分で二部グラフ判定
        * 二部グラフじゃない連結成分があったなら、終了。もうだめ。おわり。
        * 二部グラフ判定しつつ、白組と黒組に分ける
            * 白組の点から足せる辺は
                * 今見てる連結成分以外の全頂点 = 全頂点数 - 今見てる連結成分の頂点数
                * 今見てる連結成分内の黒組の頂点数 - 今見てる頂点から既に引かれてる辺の数
            * 黒組は逆に取ればOK
                * 白、黒どっちも取っちゃうとa-bの辺とb-aの辺を数えちゃうので、2で割る点に注意

# ソースコード(初心者向け)
```python:D.py
from collections import deque

N, M = map(int, input().split())
L = [[] for _ in range(N)]
for i in range(M):
    u, v = map(int, input().split())
    u -= 1
    v -= 1
    L[u].append(v)
    L[v].append(u)

color_d = dict()
ans = 0

for i in range(N):
    if i in color_d: continue
    que = deque()
    que.append(i)

    set_0 = set()
    set_1 = set()
    color_d[i] = 0

    while que:
        now_pos = que.popleft()
        now_color = color_d[now_pos]

        if now_color == 0:
            set_0.add(now_pos)
        else:
            set_1.add(now_pos)

        for next_pos in L[now_pos]:
            if next_pos not in color_d:
                color_d[next_pos] = now_color ^ 1
                que.append(next_pos)
            elif color_d[next_pos] == now_color:
                print(0)
                exit()

    len_0 = len(set_0)
    len_1 = len(set_1)
    other_node_cnt = N - (len_0 + len_1)

    for node in set_0:
        ans += other_node_cnt + len_1 - len(L[node])
    for node in set_1:
        ans += other_node_cnt + len_0 - len(L[node])
print(ans // 2)

```

# 上級者向けtips
* [にｃｋなめ氏から頂いた有り難いリプ](https://twitter.com/nickname959198/status/1604163801120591872?s=20&t=Ul6VaS8g5ptuaTJVB7SaBw)
    * 二部グラフ判定に関しては、UnionFindで全点に対して一気に出来るよ
    * 加えて、UnionFindのroot数を数えていくとそれぞれの連結成分の白/黒が数えられるよ
    * 全頂点間に辺を張った上で、張っちゃいけない辺を数えていく逆転の発想できれいにまとまるよ
    * TODO:要追記