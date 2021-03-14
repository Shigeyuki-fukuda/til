# 論理積代入 (&&=)

論理積代入(x &&= y)演算子は、`xがtruthyである場合` にのみ代入する演算子 :memo:

```js
> let x = true;
> x &&= "hoge";
> console.log(x);
hoge

> let y = false;
> y &&= "fuga";
> console.log(y);
false
```