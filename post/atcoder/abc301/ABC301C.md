---
title: ABC301 C - AtCoder Cards
date: 2023-05-13
draft: false
summary: dictで落とすだけ
tags: [ABC,ABC301,C,300点,Counter]
katex: math
---

* S,Tの文字種毎にカウンター
* 'atcoder'に含まれない文字については
	* SとTで個数が一致していないと駄目
* 'atcoder'に含まれる文字については、
	* SとTで個数が少ない方の@の数から、差分を引いていく
* 最終的に@の数が足りてたらOK

```Python
from collections import Counter  
  
S = input()  
T = input()  
Sc = Counter(S)  
Tc = Counter(T)

for c in 'abcdefghijklmnopqrstuvwxyz':  
    if c in 'atcoder':  
        if Sc[c] < Tc[c]:  
            Sc['@'] -= Tc[c] - Sc[c]  
        else:  
            Tc['@'] -= Sc[c] - Tc[c]  
    else:  
        if Sc[c] != Tc[c]:  
            Sc['@'] -= 10 ** 18  
  
print('Yes' if Sc['@'] >= 0 and Tc['@'] >= 0 else 'No')
```