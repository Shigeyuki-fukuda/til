# RSpecのchangeマッチャーで複数の要素の変更前後を検証したい場合

## 復習：基本編

- X すると Y が A から B に変わることを期待する

```ruby
expect{ user.destroy }.to change{ User.count }.from(A).to(B)
```

- `by` を使うと元の値は気にせず何個変わったかの相対値を検証する

```ruby
expect{ user.destroy }.to change{ User.count }.by(-1)
```

## 応用編：複数のchange

- `.and change` でチェーンすれば :ok_hand:


```ruby
expect{ Hoge.call }
.to change(Hoge, :count).from(0).to(1)
.and change(Fuga, :count).from(0).to(1)
```