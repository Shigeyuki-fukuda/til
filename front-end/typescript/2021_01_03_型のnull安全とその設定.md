# 型のnull安全とその設定

## tsconfig.jsonの設定

TypeScriptはデフォルトで全ての型に `null` と `undefined` を代入出来てしまうので、コンパイラオプションを `tsconfig.json` に追加する必要がある。

```ts
{
  "strictNullChecks": true
}
```

これで `null` と `undefined` と他の型が区別されるようになる。

```ts
$ ts-node
> const foo: string = null;
[eval].ts:1:7 - error TS2322: Type 'null' is not assignable to type 'string'. 1 const foo: string = null;

> const bar: number = undefined;
[eval].ts:1:7 - error TS2322: Type 'undefined' is not assignable to type 'number'.
1 const bar: number = undefined;
```
