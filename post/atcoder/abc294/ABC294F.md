---
title: ABC294 F - Sugar Water 2
date: 2023-03-19
draft: false
summary: にぶたんを使いこなすやつ
tags: [ABC,ABC294,F,500点,数学,二分探索]
katex: math
---
* 二分探索で答え決め打ち＋条件判定を二分探索
* 砂糖の量とお水の量と、濃度の関係がよく分かってないため無事死亡

```Python
import bisect  
  
N, M, K = map(int, input().split())  
takahashi_L = []  
for i in range(N):  
    A, B = map(int, input().split())  
    takahashi_L.append([A, B])  
aoki_L = []  
for i in range(M):  
    C, D = map(int, input().split())  
    aoki_L.append([C, D])  
  
  
# 目標濃度とお水の量を入れると、必要なお砂糖の量を返してくれる凄いやつだよ！  
def sugar_check(noudo, water):  
    sugar = noudo * water / (1 - noudo)  
    return sugar  
  
  
# 目標濃度を設定したら、青木氏の砂糖水それぞれで、お砂糖がどれだけ余ってる/不足してるかを計算してソートして配列出力してくれる凄いやつだよ！  
def make_aoki_L(noudo):  
    L = []  
    for sugar, water in aoki_L:  
        target_sugar = sugar_check(noudo, water)  
        diff_sugar = sugar - target_sugar  
        L.append(diff_sugar)  
    L.sort()  
    return L  
  
  
def check(noudo):  
    # 目標濃度に対して、青木くんの持ってる砂糖水のお砂糖が余ってる/不足してるを一旦作るよ（前処理）  
    tmp_L = make_aoki_L(noudo)  
    cnt = 0  
    # 高橋くんの砂糖水を1本ずつ見ていくよ！  
    for t_sugar, t_water in takahashi_L:  
        # 高橋くんのお水で、目標濃度を作るにはこれだけのお砂糖が必要！  
        need_sugar = sugar_check(noudo, t_water)  
        # 必要なお砂糖に対して、どれだけ足りてない？  
        diff_sugar = need_sugar - t_sugar  
  
        # 高橋くんの砂糖水+青木くんの砂糖水は、二人のお砂糖余りが0を超えてるなら目標濃度を超える！  
        # 0ならぴったり目標濃度！ここでもう1回にぶたんでlogN！  
        # 今見てる高橋くんの砂糖水と合わせて目標濃度を達成できる青木くんの砂糖水は何本ある？  
        cnt += M - bisect.bisect_left(tmp_L, diff_sugar)  
  
    # 最終的に目標濃度の砂糖水、K本作れる？  
    if cnt >= K:  
        return True  
    return False  
  
def meguru_bisect(ok, ng):  
    for i in range(100):  
        mid = (ok + ng) / 2  
        if check(mid):  
            ok = mid  
        else:  
            ng = mid  
    return ok * 100  
  
  
print(meguru_bisect(0, 1))
```