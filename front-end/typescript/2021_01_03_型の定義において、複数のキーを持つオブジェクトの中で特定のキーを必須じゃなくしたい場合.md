# 型の定義において、複数のキーを持つオブジェクトの中で特定のキーを必須じゃなくしたい場合

## 必須になってしまう定義の例

```ts
type C = { foo: number; baz: boolean; };
// fooのキーがないオブジェクトをCの型の変数に代入しようとするとエラーになる
let c: C = { baz: true };
// [eval].ts:2:5 - error TS2741: Property 'foo' is missing in type '{ baz: true; }' but required in type 'C'.
```

## 必須じゃない定義の例

キー名の後に `?` をつけると任意のキーになる :memo:

```ts
type C = { foo?: number; baz: boolean; };
let c: C = { baz: true };
console.log(c);
// { baz: true }
```
