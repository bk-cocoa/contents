---
title: ABC294 E - 2xN Grid
date: 2023-03-19
draft: false
summary: ランレングス圧縮を理解していますか？
tags: [ABC,ABC294,E,500点,RLE]
katex: math
---

* 逆ランレングス圧縮みたいな。
* Listだから後ろから見ていくと楽

```Python
L, N1, N2 = map(int, input().split())  
  
L1 = []  
L2 = []  
for i in range(N1):  
    v, l = map(int, input().split())  
    L1.append([v, l])  
  
for i in range(N2):  
    v, l = map(int, input().split())  
    L2.append([v, l])  
  
ans = 0  
idx = 0  
  
while True:  
    if L == 0:  
        break  
    v1, l1 = L1.pop()  
    v2, l2 = L2.pop()  
  
    if v1 == v2:  
        if l1 == l2:  
            ans += l1  
            L -= l1  
        elif l1 < l2:  
            ans += l1  
            L -= l1  
            L2.append([v2, l2 - l1])  
        else:  
            ans += l2  
            L -= l2  
            L1.append([v1, l1 - l2])  
    else:  
        if l1 == l2:  
            L -= l1  
        elif l1 < l2:  
            L -= l1  
            L2.append([v2, l2 - l1])  
        else:  
            L -= l2  
            L1.append([v1, l1 - l2])  
print(ans)
```

