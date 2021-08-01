# Vue.js の useContext で取得出来るもの

nuxt.config.js に定義したものや useContext に inject したものを利用可能

```ts
// ~/plugins/notify.ts
import Vue from "vue";
import { defineNuxtPlugin } from "@nuxtjs/composition-api";

export default defineNuxtPlugin((_, inject): void => {
  inject("notify", Vue.prototype.$notify);
});
```

```js
// nuxt.config.js
const plugins = ["~/plugins/notify"];

module.exports = {
  // 中略
  plugins,
};
```

```js
const context = useContext();
context.$sentry.captureException(err);
context.$notify.error("通信に失敗しました。再度お試しください。");
```
