---
title: ABC294 B - ASCII Art
date: 2023-03-19
draft: false
summary: 全部舐めるだけ
tags: [ABC,ABC294,B,200点,全探索]
katex: math
---

* 100×100の全マスに、0~26の27種類をそれぞれ表示させるだけ
```python:B.py
H, W = map(int, input().split())  
  
chars = '.ABCDEFGHIJKLMNOPQRSTUVWXYZ'  
  
for i in range(H):  
    ans_L = []  
    row_L = list(map(int, input().split()))  
  
    for num in row_L:  
        ans_L.append(chars[num])  
    print(''.join(ans_L))
```