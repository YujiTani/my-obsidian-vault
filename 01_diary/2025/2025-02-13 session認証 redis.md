---
tags:
  - diary
  - Auth
  - redis
---

## TODO
- [ ] redisを使ったセッション認証
	- [ ] jsonで保存することで、保存データ量を増やしたい
		- [ ] セッションをいつまで保持するか、ユーザーIDとか
	- [ ] セッションIDをランダム文字列に変更する
	- [ ] クライアント側から、アクセス権限がないとみれないAPIを実装し、クッキーの有無で対応に変化をさせるようにする
- [ ] TODO2
## NOTE
### TODOの振り返り(成果について、それはなぜか)
この動画が自分のやりたいことっぽい。
セッション認証で、セッション管理データをredisに保存する
こうすれば、ネックとなっているデータベースへのクエリ発行でパフォーマンスが落ちる件の解消になりそう
[Sessions in Node #1 | Authentication in Node.js with Express and sessions | Sessions explained - YouTube](https://youtu.be/bvQah0k5-eA?si=KZd_db7usN8P0ZVh)

session情報をredisに保存する、こういった情報を保存すると良さそう
![[スクリーンショット 2025-02-13 22.42.14.png]]

新規登録のながれ表
![[スクリーンショット 2025-02-12 14.19.26 1.png]]### MEMO
メモしたいことを書く


### Wishlist
やりたいことを書く