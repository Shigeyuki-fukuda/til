# NuxtからAngularJSのページの特定のタブに直接遷移するやり方メモ

## やり方

## Nuxt側

- Nuxt側のリンクには、AngularJS側で受け取るクエリパラメータを付与する

```vue
<li v-if="hoge">
  <a
    :href="`${HOGE_URL}?tab=hoge`"
```

### AngularJS側

- 下記の例では、ページ描画前に叩かれる activate関数 を定義し、その中でNuxt側から渡したクエリパラメータを取得して、タブを切り替えている

```js
(function() {
  'use strict';

  angular
    .module('Hoge')
    .controller('FugaController', FugaController);

  FugaController.$inject = ['$scope', '$window', '$location', 'RemitStatus'];

  function FugaController($scope, $window, $location) {

  activate();

  function activate() {
    var tab = $location.search().tab;
    vm.currentTab = tab === hogeTab ? hogeTab : fugaTab;
  }
```