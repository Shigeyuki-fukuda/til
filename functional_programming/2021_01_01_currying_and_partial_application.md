# カリー化と関数の部分適用について

## 関数の部分適用とは？

カリー化された関数の一部の引数を固定して新しい関数を作ることを『関数の部分適用』と呼ぶ :memo:

## 具体例

```js
const withMultiple = (n) => (m) => n * m;
const triple = withMultiple(3)
console.log(triple(5));
```
