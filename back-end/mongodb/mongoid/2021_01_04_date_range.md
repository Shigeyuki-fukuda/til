# mongoidでの日付範囲指定構文

忘れては定期的にググってしまうのでメモ :memo:

## 構文

```rb
Model.between(created_at: [開始日付, 終了日付])
```

## 具体例

```rb
start_date = Time.zone.parse('2020-12-31 00:00:00')
end_date = Time.zone.parse('2021-01-01 23:59:59')
user = User.find_by(email: "hoge@example.com")
user.blogs.between(created_at: [start_date, end_date]).to_a;nil
```
