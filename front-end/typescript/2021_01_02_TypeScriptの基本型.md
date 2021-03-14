# TypeScriptの基本型

## Boolean型

型名は `boolean`

```js
> let isValid: boolean = true;
> isValid
true
```

## Number型

型名は `number`

```js
> let num: number = 1;
> num
1
```

## String型

型名は `string`

```js
> let color: string = "blue";
> color
'blue'
```

## Array型

型名は `array`

```js
> let list: number[] = [1, 2, 3];
> list
[ 1, 2, 3 ]

> let list: Array<number> = [1, 2, 3];
> list
[ 1, 2, 3 ]

> let beatles: Array<string> = ["paul", "john", "ringo", "george"];
> beatles
[ 'paul', 'john', 'ringo', 'george' ]
```

## Tuple型

たとえば、値を `string:` と `number:` のペアとして表したい場合

```js
> let x: [string, number] = ["blink", 182];
> x
[ 'blink', 182 ]
```

## オブジェクトに名前をつけるInterface

TypeScriptではオブジェクトの型に名前をつけることが出来、それをインターフェース(Interface)と呼ぶ :memo:

```js
interface Color {
  readonly rgb: string;
  opacity: number;
  name?: string;
}

const turquoise: Color = { rgb: '00afcc', opacity: 1 };
turquoise.name = 'Turquoise Blue';
turquoise.rgb = '03c1ff'; // error TS2540: Cannot assign to 'rgb' because it is a read-only property.
```

`readonly` 修飾子を つけたプロパティは書き換え不可になる。
それからプロパティ名の末尾に `?` をつけると、そのプロパティは省略可能になる。

## Interfaceのプロパティ定義をより柔軟にした場合

```js
interface Status {
  level: number;
  maxHP: number;
  maxMP: number;
  [attr: string]: number;
}

const myStatus: Status = {
  level: 99,
  maxHP: 999,
  maxMP: 999,
  attack: 999,
  defense: 999
};
```

インターフェースの内部、4つ目が任意のキーのプロパティ値を定義していて、これを `インデックスシグネチャ` と呼ぶ。
そのおかげで、 `attack` と `defence` を定義することが出来ている。
インデックスシグネチャのキーに使える型は `string` と `number` の2種類のみなので注意 :memo:

## Enum型

```js
enum Pet {
  Cat='Cat',
  Dog='Dog',
  Rabbit='Rabbit',
}
let Tom: Pet = Pet.Cat;

// 同じ文字列でも型が違うのでエラーになる
Tom = 'Dog'; // [eval].ts:21:1 - error TS2322: Type '"Dog"' is not assignable to type 'Pet'.

// enumのPet.Cat、Pet.Dog、Pet.Rabbit のいずれかなら型が一致するので代入可能
Tom = Pet.Dog;
```

## リテラル型

任意の文字列(数値)以外を許さない型で、演算子 `|` で並べることによってあたかも列挙型のように扱える :memo:

```js
let nirvana: 'Kurt' | 'Dave' | 'Krist' = 'Kurt';

// 代入出来るパターン
nirvana = 'Dave';
// 代入出来ないパターン
nirvana = 'Pat'; // [eval].ts:5:1 - error TS2322: Type '"Pat"' is not assignable to type '"Kurt" | "Dave" | "Krist"'.
```

## Any、Unknown、Never型

TypeScriptではバージョン3.0から `unknown` という型が追加された。`unknown` は `any` の型安全版で任意の型の値を代入できる点は同じ。しかし、それ自体は何のプロパティもプロトタイプメソッドも持たない型になっている。

```js
const str = `{"id": 1, "username": "john_doe"}`; const user: unknown = JSON.parse(str);
console.log(user.id, user.address.zipcode);
// error TS2339: Property 'id' 'address' does not exist on type 'unknown'.

// 上記の例ではエラーにはなってしまうので、その値の型を特定する処理を追加すればコンパイルも通る上、型安全も保証される理想の状態が実現出来る(『型ガード』という手法)。
```

`never` は値を持たず、何も代入出来ない型。
`never` に特定の値が代入されそうな分岐処理になっている場合はコンパイル出来ないためエディタ上にエラーが表示される。そのため `never` を使うことで、 `case文の漏れ` を未然にチェック出来たりする :memo:

```js
const greet = (friend: 'Serval' | 'Caracal' | 'Cheetah') => {
  switch (friend) {
    case 'Serval':
      return `Hello, ${friend}!`;
    case 'Caracal':
      return `Hi, ${friend}!`;
    case 'Cheetah':
      return `Hiya, ${friend}!`;
    default: {
      const check: never = friend;
    }
  }
};
console.log(greet('Serval')); // Hello, Serval!
```
