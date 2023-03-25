---
title: ABC294 A - Filter
date: 2023-03-19
draft: false
summary: 全部舐めるだけ
tags: [ABC,ABC294,A,100点,全探索]
katex: math
---

* 全探索
* Aを全部舐めて、偶数だけ拾っていく
```python:A.py
N = int(input())  
A_L = list(map(int, input().split()))  
ans_L = []  
for a in A_L:  
    if a % 2 == 0:  
        ans_L.append(a)  
print(*ans_L)
```

