# JSON.parse時のオプション `symbolize_names: true` について

## 使用例

`JSON.parse(json, symbolize_names: true)` の形式で使用する :memo:

```ruby
json = JSON.generate(User.new(1, "tanaka"))
=> "{\"json_class\":\"User\",\"id\":1,\"name\":\"tanaka\"}"

JSON.parse(json)
=> {"json_class"=>"User", "id"=>1, "name"=>"tanaka"}

JSON.parse(json, symbolize_names: true)
=> {:json_class=>"User", :id=>1, :name=>"tanaka"}
```

これをすることでJSON.parseの結果のkeyをsymbolにすることが出来る :memo: