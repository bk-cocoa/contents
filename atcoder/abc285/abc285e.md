---
title: ABC285 E - Work or Rest
date: 2023-01-15
draft: False
summary: DPに落とし込むまで難しいでござる…
tags: [ABC,ABC285,E,500点,DP]
katex: math
---
# 問題
[ABC285 E - Work or Rest](https://atcoder.jp/contests/abc285/tasks/abc285_e)

# お気持ち
* B問題と同じく、問題文をちゃんと読んで、実験して、しっかりDPに落とし込めたらこんなに簡単だった…
* 前処理ちゃんと丁寧にできたら、所詮1次元DPだった…ううう、悔しい…

# ソースコード
```python:E.py
N = int(input())
A_L = list(map(int, input().split()))

if N == 1:
    print(0)
    exit()
elif N == 2:
    print(A_L[0])
    exit()

B_L = []
for i in range(N):
    B_L.append(A_L[i])
    B_L.append(A_L[i])
accum_L = [0]
for b in B_L:
    accum_L.append(accum_L[-1] + b)

dp = [0] * (N + 5)
dp[1] = accum_L[1]
dp[2] = accum_L[2]
dp[3] = accum_L[3]

for renkin in range(4, N):
    dp[renkin] = accum_L[renkin]

    for i in range(1, renkin - 1):
        dp[renkin] = max(dp[renkin], dp[i] + dp[renkin - 1 - i])
print(dp[N - 1])
```