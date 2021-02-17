# Node.jsのREPLのエディターモード

## 概要

Node.jsのREPLはターミナルで `node` を打てば起動するものの複数行のコードはやや見づらい。
そこで `.editor` とREPL起動時に入力すると長いコードの入力に便利なエディタモードを利用することが出来る。
なお、終了したい場合は `Ctrl + D` で終了出来る。

```js
$ node
> .editor
// エディタモード起動
let total2 = 0;
for (let i = 1; i <= 10; i++) {
  total2 += i
  console.log(`${i}までの和: ${total2}`)
}
total2

// Ctrl + D 押下後
1までの和: 1
2までの和: 3
3までの和: 6
4までの和: 10
5までの和: 15
6までの和: 21
7までの和: 28
8までの和: 36
9までの和: 45
10までの和: 55
55
```