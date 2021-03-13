# Tailwind CSSをJSフレームワークを経由せず利用する手順

## 手順

- package.jsonの生成

```bash
$ npm init -y
```

- プラグインのインストール

```bash
$ npm install tailwindcss@latest postcss@latest autoprefixer@latest
```

- 構成ファイルの作成

```bash
$ npx tailwindcss init
```

- ルートディレクトリにビルド用ディレクトリの `src` を追加し、そこに以下の内容で `tailwind.css` を作成

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

- 以下のコマンドでビルドすると整形されたtailwindファイルが出力される

```bash
$ npx tailwindcss-cli@latest build ./src/tailwind.css -o ./dist/tailwind.css
```

- `dist` 配下のビルド済みファイルをHTMLから読み込めばOK

```html
<link rel="stylesheet" href="dist/tailwind.css">
```

## 参考

https://qiita.com/Masahiro111/items/62a4927be42a8c06bc79