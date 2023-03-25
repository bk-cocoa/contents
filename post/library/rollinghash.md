---
title: 黒ココア式RollingHash
date: 2023-01-10T00:00:00+09:00
draft: false
tags: [競プロ,ライブラリ,BlackCocoaRollingHash]
summary: 文字列一致判定がぴゃっと出来る強いやつ
katex: math
---
## ソースコード
* 正直、[これ](https://qiita.com/keymoon/items/11fac5627672a6d6a9f6)をPython移植しただけのやつ
* あんまり中身が何してるのかはわかってないけど、爆速、っぽい…
    * [参考](https://atcoder.jp/contests/abc284/submissions/37891421)
    * `(1<<61)-1` $= 2305843009213693951 > 2 \times 10^{18}$

```python:BlackCocoaRollingHash.py
class BlackCocoaRollingHash():
    def __init__(self, s, base=37, mod=(1 << 61) - 1):
        self.mask30 = (1 << 30) - 1
        self.mask31 = (1 << 31) - 1
        self.mod = mod
        self.base = base
        self.mask61 = (1 << 61) - 1
        self.positivizer = self.mod * ((1 << 3) - 1)
        l = len(s)
        self.pw = pw = [1] * (l + 1)
        self.h = h = [0] * (l + 1)
        v = 0
        for i in range(l):
            self.h[i + 1] = v = self.calcmod(self.mul(v, base) + ord(s[i]))
        v = 1
        for i in range(l):
            self.pw[i + 1] = v = self.calcmod(self.mul(v, base))

    def get(self, start, length):
        return self.calcmod(self.h[start + length] + self.positivizer - self.mul(self.h[start], self.pw[length]))

    def mul(self, a, b):
        au = a >> 31
        ad = a & self.mask31
        bu = b >> 31
        bd = b & self.mask31
        mid = ad * bu + au * bd
        midu = mid >> 30
        midd = mid & self.mask30
        return self.calcmod(au * bu * 2 + midu + (midd << 31) + ad * bd)

    def calcmod(self, x):
        xu = x >> 61
        xd = x & self.mask61
        res = xu + xd
        if res >= self.mod:
            res -= self.mod
        return res
```