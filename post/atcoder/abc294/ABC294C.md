---
title: ABC294 C - Merge Sequences 
date: 2023-03-19
draft: false
summary: 実は座標圧縮
tags: [ABC,ABC294,C,300点,座標圧縮]
katex: math
---

* AとBを混ぜてCにして、index拾っていく作業
* やってることとしては #座標圧縮 のイメージ
```Python
from collections import defaultdict  
  
N, M = map(int, input().split())  
A_L = list(map(int, input().split()))  
B_L = list(map(int, input().split()))  
  
C_L = A_L + B_L  
C_L.sort()  
ans_A_L = []  
ans_B_L = []  
index_d = defaultdict(int)  
for i, c in enumerate(C_L, 1):  
    index_d[c] = i  
  
for a in A_L:  
    ans_A_L.append(index_d[a])  
for b in B_L:  
    ans_B_L.append(index_d[b])  
print(*ans_A_L)  
print(*ans_B_L)
```