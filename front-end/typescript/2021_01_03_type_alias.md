# 型エイリアス

TypeScriptにはクラスやオブジェクトの型を定義出来るインターフェースの他に任意の型に別名を与えて再利用出来る `型エイリアス(Type Alias)` というものがある。

```ts
type Unit = 'USD' | 'EUR' | 'JPY' | 'GBP';

type TCurrency = {
  unit: Unit;
  amount: number;
};

interface ICurrency {
  unit: Unit;
  amount: number;
};

const jpy: TCurrency = { unit: 'JPY', amount: 1000 };

const usd: ICurrency = { unit: 'USD', amount: 100 };

> jpy
{ unit: 'JPY', amount: 1000 }
> usd
{ unit: 'USD', amount: 100 }
```

https://typescript-jp.gitbook.io/deep-dive/type-system#eiriasutype-alias
