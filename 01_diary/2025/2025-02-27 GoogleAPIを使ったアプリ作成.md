---
tags:
  - diary
---

## TODO
- [ ] TODO1
- [ ] TODO2
## NOTE
### TODOの振り返り(成果について、それはなぜか)
https://maps.googleapis.com/maps/api/directions/json?origin=東京都庁&destination=東京タワー&key=YOUR_API_KEY

このようなデータでアクセスすることで、ルート表示に必要なJSONが返ってくる
1. 現在地(origin)を取得して、その後マップをまず描画する
2. マップから目的地を入力してもらう
3. originと目的地を入力して、APIを叩くするとルート表示用のJSONを取得できる
4. 


### MEMO
メモしたいことを書く
[scriptタグで行っていることを、javascriptファイルに記述する方法]
```
<script 
  src="https://maps.googleapis.com/maps/api/js
  ?key=YOUR_API_KEY                             <!-- (1) APIキー -->
  &callback=initMap                             <!-- (2) コールバック関数 -->
  &libraries=geometry"                          <!-- (3) 追加ライブラリ -->
  async                                         <!-- (4) 非同期読み込み -->
  defer>                                        <!-- (5) 遅延実行 -->
</script>
```


### Wishlist
やりたいことを書く
