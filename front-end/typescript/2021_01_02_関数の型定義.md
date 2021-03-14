# 関数の型定義

## 関数の型定義における設定の注意点

TypeScript ではコンパイラオプションに `noImplicitAny` が指定されてないと、引数の型定義がなくても暗黙の内に `any` 型があてがわれてコンパイルが通ってしまうので、まずは設定ファイルの `tsconfig.json` でそのオプションを有効にすること :memo:

`tsconfig.json`

```ts
{
  "noImplicitAny": true,
}
```

## 引数と戻り値の型を別々に定義する場合

```ts
// function declaration statement
{
  function add(n: number, m: number): number {
    return n + m;
  }
  console.log(add(2,4)); //6
}

// function keyword expression
{
  const add = function(n: number, m: number): number {
    return n + m;
  };
  console.log(add(5,7)); //12
}

// arrow function expression
{
  const add = (n: number, m: number): number => n + m;
  const hello = (): void => {
    console.log('Hello!');
  };
  console.log(add(8,1)); //9
  hello(); // Hello!
}
```

## 引数と戻り値をまとめて定義する方法

関数を『呼び出し可能オブジェクト(Callable Object)』 として定義する :memo:

```ts
// callable object type
{
  interface NumOp {
    (n: number, m: number): number;
  }
  const add: NumOp = function (n, m) {
    return n + m;
  };
  const subtract: NumOp = (n, m) => n - m;
  console.log(add(1, 2)); // 3
  console.log(subtract(7,2)); //5
}

// in-line
{
  const add: (n: number, m: number) => number = function (n, m) {
    return n + m;
  };
  const subtract: (n: number, m: number) => number = (n, m) => n - m;
  console.log(add(3, 7)); // 10
  console.log(subtract(10, 8)); // 2
}
```

前者がインターフェースとして呼び出し可能オブジェクトを定義し、それを関数式に適用したもの。後者はそれをアロー型アノテーションによってインラインで行ってるもの。

## 関数の型宣言にジェネリクスを用いる記法

`T` は型引数(Type Parameter)のことで、関数に渡す引数と同じで、任意の型を `<>` によって引数として渡すことで、その関数の引数や戻り値の型に適用出来るようになる :memo:

以下の例では `T` は 型推論によって number、次の例では `string` になってる

```ts
> const toArray = <T>(arg1: T, arg2: T): T[] => [arg1, arg2];
> toArray(8, 3);
// [8,3]

// 型が統一されているのでエラーにならない
> toArray('foo', 'bar'); [ 'foo', 'bar' ]

// 型が統一されていないのでエラーになる
> toArray(5, 'bar');
[eval].ts:4:12 - error TS2345: Argument of type '"bar"' is not assignable to parameter of type
'number'.
```

このようにデータの型に束縛されないよう型を抽象化してコードの再利用性を向上させつつ、 静的型付け言語の持つ型安全性を維持するプログラミング手法を『ジェネリックプログラミング
(Generic Programming)』と呼ぶ。

そして型引数を用いて表現するデータ構造のことを『ジェネリクス(Generics)』と言う。

## TypeScriptで可変長引数に型を設定する方法

```ts
const toArrayVariably = <T>(...args: T[]): T[] => [...args];

// コンパイルが通るパターン
> toArrayVariably(1, 2, 3, 4, 5); [1,2,3,4,5]

// コンパイルが通らないパターン
> toArrayVariably(6, '7', 8);
[eval].ts:3:20 - error TS2345: Argument of type '"7"' is not assignable to parameter of type
'number'.
```
