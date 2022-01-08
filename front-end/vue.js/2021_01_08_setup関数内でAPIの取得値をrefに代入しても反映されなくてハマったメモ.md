# setup関数内でAPIの取得値をrefに代入しても反映されなくてハマった時の解決法メモ

## 発生事象

APIのJSONからは金額の整数 `8000` が返っているが、それを入れる `orderPrice.value` は初期値の `0` のままでsetup関数内でその値を `¥8,000` にカンマ変換したいのに出来ない。

```js
setup() {

  const {
    orderPrice,
    fetchOrder,
  } = useOrder();

  // APIから値を取得
  fetchOrder();

  let commaSeparatedOrderPrice = '';

  if (orderPrice.value != null) {
    commaSeparatedOrderPrice = getCommaSeparatedNumber(orderPrice.value);
  }
```

## 解決法

computed(() => {})で値を監視する

```js
setup() {

  const {
    orderPrice,
    fetchOrder,
  } = useOrder();

  // APIから値を取得
  fetchOrder();

  const commaSeparatedOrderPrice = computed(() => {
    if (orderPrice.value != null) {
      return getCommaSeparatedNumber(orderPrice.value);
    }
    return '';
  });
```