---
title: ABC301 C - AtCoder Cards
date: 2023-05-13
draft: false
summary: 全頂点間の距離を求めてbitDP
tags: [ABC,ABC301,E,475点,bitDP]
katex: math
---
* 実装重いグリッド問題
* 制約は緩め、やりたいことは簡単、実装がただ重い
	* スタート、ゴール含めて必要な頂点は20箇所
	* マップの広さは300 * 300
		* 全頂点(20箇所)からBFSかけて、全頂点間の距離を出そう(パート1)
	* bitDPで、「スタートから、どのお菓子取ってゴールに行く？」の全パターンを試す感じ
		* bitDPが苦手なのもありただただ苦行
* bitDPは基本構成をライブラリ化するべきか… #TODO

```Python
from collections import deque  
  
H, W, T = map(int, input().split())  
grid_L = []  
pos_d = dict()  
for i in range(H):  
    grid_L.append(list(input()))  
    grid_L[-1].append('#')  
grid_L.append(['#'] * (W + 1))  
  
s_pos = []  
g_pos = []  
o_pos = []  
  
for r in range(H):  
    for c in range(W):  
        if grid_L[r][c] == 'S':  
            s_pos.append((r, c))  
        elif grid_L[r][c] == 'G':  
            g_pos.append((r, c))  
        elif grid_L[r][c] == 'o':  
            o_pos.append((r, c))  
  
dr = [[1, 0], [0, 1], [-1, 0], [0, -1]]  
inf = 10 ** 18  
  
o_cnt = len(o_pos)  
  
  
def bfs(pos):  
    que = deque()  
    que.append(pos)  
    dist_L = [[inf] * (W + 1) for i in range(H + 1)]  
    dist_L[pos[0]][pos[1]] = 0  
  
    while que:  
        now_x, now_y = que.popleft()  
        for dx, dy in dr:  
            if grid_L[now_x + dx][now_y + dy] == '#':  
                continue  
            if dist_L[now_x + dx][now_y + dy] != inf:  
                continue  
            if dist_L[now_x][now_y] + 1 > T:  
                continue  
            dist_L[now_x + dx][now_y + dy] = dist_L[now_x][now_y] + 1  
            que.append((now_x + dx, now_y + dy))  
    return dist_L  
  
  
start_dist = bfs(s_pos[0])  
goal_dist = bfs(g_pos[0])  
  
if start_dist[g_pos[0][0]][g_pos[0][1]] == inf:  
    print(-1)  
    exit()  
  
o_dist = [[inf] * o_cnt for i in range(o_cnt)]  
  
for i, prev_pos in enumerate(o_pos):  
    tmp = bfs(prev_pos)  
    for j, next_pos in enumerate(o_pos):  
        o_dist[i][j] = tmp[next_pos[0]][next_pos[1]]  
        o_dist[j][i] = tmp[next_pos[0]][next_pos[1]]  
  
inf = 10 ** 6  
dp = [[inf] * o_cnt for i in range(1 << o_cnt)]  
  
for i in range(o_cnt):  
    x, y = o_pos[i]  
    if start_dist[x][y] == inf:  
        continue  
    dp[1 << i][i] = start_dist[x][y]  
  
for status in range(1 << o_cnt):  
    for pos in range(o_cnt):  
        if dp[status][pos] == -1:  
            continue  
  
        for next_pos in range(o_cnt):  
            if pos == next_pos: continue  
            if o_dist[pos][next_pos] == inf: continue  
            dp[status | 1 << next_pos][next_pos] = min(dp[status | 1 << next_pos][next_pos],  
                                                       dp[status][pos] + o_dist[pos][next_pos])  
ans = 0  
  
for status in range(1 << o_cnt):  
    for last_pos in range(o_cnt):  
        if dp[status][last_pos] == inf: continue  
        if dp[status][last_pos] + goal_dist[o_pos[last_pos][0]][o_pos[last_pos][1]] > T: continue  
        ans = max(ans, bin(status).count("1"))  
print(ans)
```