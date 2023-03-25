---
title: ABC283 D - Scope
date: 2022-12-24
draft: False
summary: 文字列を見ていったり消したりするやつ
tags: [ABC,ABC283,D,400点,文字列,stack,本番AC]
katex: math
---
# 問題
[ABC283 D - Scope](https://atcoder.jp/contests/abc283/tasks/abc283_d)

# お気持ち
* テストケースが甘くて、嘘解法があっさり通ったり、制約違反？があったりと問題の問題
* `)`が出た時に、直近の`(`以降で出てきた文字を箱から削除していく
* それ以外なら文字を箱に入れていく
* 箱に同じ文字を入れた瞬間、**chokudai氏の意識が刈り取られることになる**
* アルファベットを箱に入れる時に、スタックも作る
* スタックには全部の文字(`アルファベット, (, )`)を入れる
    * `)`が来た時、スタックから`(`が出るまで文字を全部吐き出す
    * スタックから出てきた文字を全部箱から削除する
* やってることはCとそんなに変わらない…？
* これで1ペナ出したのはとっても痛い…ぐぅ…

# ソースコード
```python:D.py
S = input()
ans_flg = True

box_s = set()
stack = []
for s in S:

    if s == ')':
        while True:
            if stack[-1] == '(':
                stack.pop()
                break
            box_s.discard(stack.pop())
    else:
        stack.append(s)
        if s != '(' and s in box_s:
            ans_flg = False
            break
        box_s.add(s)

print('Yes' if ans_flg else 'No')
```
