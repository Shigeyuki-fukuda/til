# webpack-dev-serverを起動しようとするとError: Cannot find module 'webpack-cli/bin/config-yargs' が発生する場合

2020年10月10日にwebpackのバージョン５がリリースされた影響の模様 :memo:

それに伴って、webpackのローカルサーバーを起動する場合は `webpack-dev-server` コマンドではなく `webpack serve` コマンドを実行する必要がある模様 :eyes: 

## webpack5だと動かない書き方

`package.json`

```js
{
  ...
  "scripts": {
    ...
    "start": "webpack-dev-server"
  },
  ...
}
```

## webpack5で動く書き方

`package.json`

```js
{
  ...
  "scripts": {
    ...
    "start": "webpack serve"
  },
  ...
}
```

ただし、webpack serveコマンドは内部的にwebpack-dev-serverを使用するので、webpack-dev-serverはインストールしておく必要はあるので注意。

## その他参考

- [【webpack-dev-server】Cannot find module 'webpack-cli/bin/config-yargs'【webpack-cli4系】](https://qiita.com/whiteraccoon/items/f0675297fce333ac9474)
- [Webpack初心者がWebpack、Babelの設定でハマった点](https://qiita.com/uwattotaitai/items/35ab2f248f53faa98fe3)