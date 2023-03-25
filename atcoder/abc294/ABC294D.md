---
title: ABC294 D - Bank
date: 2023-03-19
draft: false
summary: 誤読したけど冷静に考えたら簡単
tags: [ABC,ABC294,D,400点,heap]
katex: math
---

* 問題文300回読め
* 声に出して読め
* heapから要素を削除する時はsetとかdictとか使う小技

```Python
import heapq  
  
N, Q = map(int, input().split())  
  
first_L = list(range(1, N + 1))  
first_L.sort()  
called_L = []  
recept_s = set()  
  
for i in range(Q):  
    query = list(map(int, input().split()))  
  
    # 一番番号小さい人呼ぶ  
    if query[0] == 1:  
        call_num = heapq.heappop(first_L)  
        called_L.append(call_num)  
  
    # 呼ばれている中で、xの人が受付に行く  
    elif query[0] == 2:  
        x = query[1]  
        recept_s.add(x)  
  
    # 既に呼ばれている、かつ、受付にいっていない人の中で、最も小さい番号の人が”””再度呼ばれる””””””””””””  
    else:  
        while True:  
            x = heapq.heappop(called_L)  
            if x in recept_s:  
                continue  
            else:  
                print(x)  
                break  
        heapq.heappush(called_L, x)
```