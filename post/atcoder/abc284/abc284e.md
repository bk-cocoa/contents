---
title: ABC284 E - Count Simple Paths
date: 2023-01-07
draft: False
summary: DFSで数え上げるやつ
tags: [ABC,ABC284,E,500点,グラフ,数え上げ,DFS]
katex: math
---
# 問題
[ABC284 E - Count Simple Paths](https://atcoder.jp/contests/abc284/tasks/abc284_e)

# お気持ち
* DFSしろ！！！数え上げろ！！！
* $min(K,10^6)$なので、$10^6$になった瞬間打ち切ってOK！！！
* pathの持ち方とかは、まぁ、何かお好みで…
    * 公式解説見てるけど、dfsでパスを持つ必要はないのでは、と思ったり…？
* 再帰で書いたからpythonで投げようね気をつけようね
* $10^6$超えた瞬間終わらせるから、計算量としては10^6でいい、のかなぁ？

# ソースコード
```python:E.py
import sys
sys.setrecursionlimit(10 ** 6)

N, M = map(int, input().split())
edge_L = [[] for i in range(N)]
for i in range(M):
    u, v = map(int, input().split())
    u -= 1
    v -= 1
    edge_L[u].append(v)
    edge_L[v].append(u)

ans = 0

def dfs(now, s):
    global ans
    ans += 1

    if ans >= 10 ** 6:
        print(10 ** 6)
        exit()

    for next_node in edge_L[now]:
        if next_node not in s:
            s.add(next_node)
            dfs(next_node, s)
            s.discard(next_node)

checked = set()
checked.add(0)
dfs(0, checked)
print(min(ans, 10 ** 6))
```