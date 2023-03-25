---
title: ABC285 D - Change Usernames
date: 2023-01-15
draft: false
summary: グラフに落とし込むと簡単
tags: [ABC,ABC285,D,400点,グラフ,UnionFind,本番AC]
katex: math
---

# 問題
[ABC285 D - Change Usernames](https://atcoder.jp/contests/abc285/tasks/abc285_d)

# お気持ち
* 本番は実装力ゴリ押しBFSみたいな形で通しました（無事AC）
* $S_i$は相違なる、かつ、$T_i$は相違なる、から解ること
    * 今の名前が一緒の人は居ない
    * 将来の名前が一緒になる人は居ない
* ここから名前を頂点に有向グラフを考える
* グラフまで落とせたら、後はサイクル検出でOK
    * UnionFindが早いよねぇ
        * ついでに黒ココア式UnionFindを改めて生やした
        * そのうち別記事書こう

# ソースコード
```python:D.py
class BlackCocoaUnionFind():
    def __init__(self):
        self.parents = dict()
        self.size = dict()
        self.groupcount = 0

    def add(self, s):
        if s not in self.parents:
            self.parents[s] = s
            self.size[s] = 1
            self.groupcount += 1
            return True
        return False

    def find(self, s):
        if s not in self.parents:
            self.add(s)
            return s
        if self.parents[s] == s:
            return s
        self.parents[s] = self.find(self.parents[s])
        return self.parents[s]

    def union(self, s, t):
        s = self.find(s)
        t = self.find(t)

        if s == t:
            return False

        if self.size[s] < self.size[t]:
            s, t = t, s
        self.size[s] += self.size[t]
        self.parents[t] = s

        self.groupcount -= 1
        return True

    def is_same(self, s, t):
        return self.find(s) == self.find(t)


N = int(input())
uf = BlackCocoaUnionFind()
for i in range(N):
    S, T = input().split()
    if uf.union(S, T):
        continue
    else:
        print('No')
        exit()
print('Yes')

```
