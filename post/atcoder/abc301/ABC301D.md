---
title: ABC301 D - Bitmask
date: 2023-05-13
draft: false
summary: 2進数理解してますか？
tags: [ABC,ABC301,D,400点,bit演算]
katex: math
---
* Sのうち$1$になっている桁は、確定で$2^n$使う！
* $?$になってる桁のうち、左から順に貪欲に1にしたいよね！ハイ終わり！
```Python
S = input()
N = int(input())
  
num = 0
L = []
  
for i, c in enumerate(S[::-1]):
    if c == '1':
        num += 2 ** i
    elif c == '?':
        L.append(2 ** i)

L.sort(reverse=True)
for add_num in L:
	if num + add_num <= N:
	    num += add_num
  
print(num if num <= N else -1)
```