# Cookie と WebStorage に関するおさらい

|                    | サイズ                  | サーバー通信 | 有効期限               | 範囲           |
| ------------------ | ----------------------- | ------------ | ---------------------- | -------------- |
| Cookie             | 4KB                     | 毎回         | 指定期限まで           | -              |
| Local<br>Storage   | 1 オリジンあたり<br>5MB | 必要時のみ   | なし                   | オリジン単位   |
| Session<br>Storage | 1 オリジンあたり<br>5MB | 必要時のみ   | ウィンドウを閉じるまで | セッション単位 |

## LocalStorage の取得・保存・削除

```js
// 取得
localStorage.getItem(key);

// 保存
localStorage.setItem(key);

// 削除
localStorage.removeItem(key);
```
