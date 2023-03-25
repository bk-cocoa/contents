---
title: ABC283 C - Cash Register
date: 2022-12-24
draft: False
summary: 文字列置換したり数えたりするやつ
tags: [ABC,ABC283,C,300点,文字列,本番AC]
katex: math
---
# 問題
[ABC283 C - Cash Register](https://atcoder.jp/contests/abc283/tasks/abc283_c)

# お気持ち
* 先頭から入力したい気持ちが消せなかったので、一旦逆順に並べかえて、先頭から順に見ていく作業
    * 多分逆順じゃなくても変わらないよねー
    * 今見ている文字が0の時、次の文字も0なら、セットで処理
    * そうじゃないなら、1文字だけ処理
    * 本番、最後の一文字に対しても「次の文字」を要求したためREで1ペナ
        * 多分IndexError？
    * 「00」ならセットで1ボタンで消す、それ以外の数字は1ボタンで消す←多分ここが本質

# ソースコード
```python:C.py
S = input()
L = list(S)

ans = 0

while L:
    if len(L) >= 2:
        if L[-2] == '0' and L[-1] == '0':
            ans += 1
            L.pop()
            L.pop()
        else:
            ans += 1
            L.pop()
    else:
        ans += 1
        L.pop()
print(ans)
```
# 別解
* [あさか氏のreplace解](https://twitter.com/asakaakasaka/status/1606646479816650754)が頭良すぎた
* replaceの置換挙動をちゃんと理解してたらこれで一発で抜けましたね…天才…