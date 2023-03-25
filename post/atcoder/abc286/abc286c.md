---
title: ABC286 C - Rotate and Palindrome
date: 2023-01-21
draft: false
summary: 全探索するだけ
tags: [ABC,ABC286,C,300点,for文]
katex: math
---
# 問題
[ABC286 C - Rotate and Palindrome](https://atcoder.jp/contests/abc286/tasks/abc286_c)

# お気持ち
* 操作1（A円払う）を0〜N回行った際に、それぞれ何回操作2（B円払う）を行うかを愚直にチェックしていく
* なんか関数とか作ってみたりした
* 愚直だけど$O(N^2)$で全然間に合いますね！

# ソースコード
```python:C.py
from collections import deque

N, A, B = map(int, input().split())
S = input()

que = deque(list(S))

def check(q):
    cnt = 0

    for i in range(N):
        if q[i] != q[-1 - i]:
            cnt += 1
    return cnt // 2

ans = 10 ** 18

for i in range(N):
    tmp = i * A
    tmp += check(que) * B
    ans = min(ans, tmp)
    que.append(que.popleft())

print(ans)
```