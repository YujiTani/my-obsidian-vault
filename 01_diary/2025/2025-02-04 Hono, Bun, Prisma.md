---
tags:
  - diary
  - prisma
---
# TITLE
## きょうやることのメインタスク名

## プライベートTODO(今日やること)
- [ ] APIのどこかしらにエラーが発生しているので解消する
	- [ ] エラー箇所がわかりやすいように、エラーハンドリングを追加する
- [ ] Honoをデプロイする
	- [ ] デプロイ先: back4app
## NOTE
### TODOの振り返り(成果について、それはなぜか)



### MEMO
メモしたいことを書く
[[誤ってあげた.env削除]]

[[ファイル転送 rsyncコマンド]]

Bunを使ってPrismaをインストール後、通常通りの設定でgenerateするとバイナリーエラーが発生した。

binaryを指定する設定を追記し、generateし直すと動作した
```
generator client {
  provider = "prisma-client-js"
  binaryTargets = ["native", "darwin-arm64"] <- 追記
}
```

Honoをデプロイする
参考：デプロイ先
[【実演映像付き】無料で使えるサーバーレスサービス11選を徹底比較!! - YouTube](https://youtu.be/682QkAioZGk?si=PYmCEM2hmO3fo3Ev)


### Wishlist
やりたいことを書く
