---
title: 黒ココア式DoubleHeap
date: 2022-12-14
draft: false
tags: [競プロ,ライブラリ,Heapq]
summary: 最小値、最大値が取れるすごいやつ
katex: math
---

## お気持ち
- [ABC281 E](https://atcoder.jp/contests/abc281/tasks/abc281_e)が本番AC出来なかったため、悔しくて作った
- 1つのインスタンスで最小値/最大値の取得がO(logN)で出来たり、特定要素の存在確認、特定要素の削除なんかも出来るそこそこすごいやつだよ
- 計算量とかは物凄く怪しいので話半分で読んで欲しいです
- 自己責任で勝手に使って下さい
- 12/17:こっそり改名（誰も見てないでしょ…多分…！）

## ソースコード
```python:BlackCocoaHeap.py
import heapq

class BlackCocoaHeap:
    def __init__(self):
        self.minh = []
        self.maxh = []
        self.d = dict()
        self.size = 0
        self.total = 0

    def push(self, x):
        self.size += 1
        self.total += x
        heapq.heappush(self.minh, x)
        heapq.heappush(self.maxh, -x)
        if x not in self.d:
            self.d[x] = 1
        else:
            self.d[x] += 1

    def get_min(self):
        return self.minh[0]

    def get_max(self):
        return -self.maxh[0]

    def pop_min(self):
        n = self.get_min()
        self.discard(n)
        return n

    def pop_max(self):
        n = self.get_max()
        self.discard(n)
        return n

    def discard(self, x):
        if self.is_exist(x):
            self.size -= 1
            self.total -= x
            self.d[x] -= 1
            if self.d[x] == 0:
                del self.d[x]

            while len(self.minh) != 0 and self.minh[0] not in self.d:
                heapq.heappop(self.minh)
            while len(self.maxh) != 0 and -self.maxh[0] not in self.d:
                heapq.heappop(self.maxh)
            return True
        return False

    def erase(self, x, n=10 ** 18):
        if self.is_exist(x):
            if self.d[x] < n:
                n = self.d[x]
            self.size -= n
            self.total -= x * n
            self.d[x] -= n
            if self.d[x] == 0:
                del self.d[x]

            while len(self.minh) != 0 and self.minh[0] not in self.d:
                heapq.heappop(self.minh)
            while len(self.maxh) != 0 and -self.maxh[0] not in self.d:
                heapq.heappop(self.maxh)
            return n
        return 0

    def is_exist(self, x):
        if x in self.d:
            return True
        else:
            return False

    def __len__(self, x):
        return self.size

    def len(self):
        return self.size

    def types(self):
        return len(self.d)

    def sum(self):
        return self.total

    def count(self, x):
        if self.is_exist(self,x):
            return self.d[x]
        return 0
```

## 使い方
### `BCH = BlackCocoaHeap()`
BlackCocoaHeapインスタンスを生成します。初期値とかそういうのはいらないです。

### `BCH.push(item)`
BlackCocoaHeapにitemをpushします。O(logN)時間です。

### `BCH.get_min()`/`BCH.get_max()`
BlackCocoaHeapの最小値/最大値を参照します。見るだけ。  
BlackCocoaHeapの状態は変わりません。O(1)時間です。

### `BCH.pop_min()`/`BCH.pop_max()`
BlackCocoaHeapから最小値/最大値を取り出します。O(logN)時間です。  
参照→参照した値を1つ削除、の手順で取り出しています。

### `BCH.discard(item)`
BlackCocoaHeapからitemを1つだけ削除します。多分O(logN)時間です。  
削除の成功/失敗をbool値で返却します。

### `BCH.erase(item, n)`
BlackCocoaHeapからitemをn個削除します。多分O(logN)時間です。  
itemがn個未満の場合、存在するitemが全て削除されます。  
また、削除した個数を返却します。  
BlackCocoaHeapに存在するitemが0個の場合、0が返却されます。

### `BCH.is_exist(item)`
BlackCocoaHeapにitemが存在するか否かをbool値で返却します。

### `BCH.len(item)`/`len(BCH)`
BlackCocoaHeapに存在する要素の個数を返却します。

### `BCH.types()`
BlackCocoaHeapに存在する要素の種類数を返却します。

### `BCH.sum()`
BlackCocoaHeapに存在する要素の総和を返却します。

### `BCH.count(item)`
BlackCocoaHeapに存在するitemの個数を返却します。
