---
tags:
  - diary
---
# TITLE
## アプリ開発:問題作成用の管理画面
今日もTSを使ったAPIサーバーの実装方法を学んでいく
クエスト, コース, ステージ

リレーション部分、1:1、1:多、多:多
それぞれ削除された時の動きの設定

## TODO(今日やること)
- [ ] courseAPI作成
	- [ ] ルート
	- [ ] コントローラー
		- [ ] リレーション
		- [ ] 一括作成
		- [ ] N+1
	- [ ] バリデーション
	- [ ] リクエスト
- [ ] テスト作成?
	- [ ] 作成したAPIのテストコードの書き方の練習
	- [ ] Jest
- [ ] 認証機能?
	- [ ] Basic
	- [ ] メルアド・パスワード認証
	- [ ] CORS
	- [ ] セッション・クッキー
	- [ ] トークン認証
## NOTE
### TODOの振り返り(成果について、それはなぜか)


### MEMO
prismaでは、単体取得系のメソッドでは取得できなくてもnullを返すようだ
- findUnique
- findFirst

なのでnullじゃない値を返したい場合は、エラーハンドリングが必要

```
      const quest = await prisma.quest.findUnique({
        where: {
          id: Number(req.params.id),
          deletedAt: null
        }
      })

      if (!quest) {
        return res.status(404).json({ 
            message: 'リソースが見つかりません' 
        });
      }

```

### Wishlist
アプリ開発:問題作成用の管理画面
- APIのレスポンスを返却するロジックをもう少し共通化したい
  レスポンスを共通化できるので、あとの開発がだんだん楽になるかも？
``` 基本形
{
	response_id: uuid <- ログ追跡用のUUIDを付与したい 使い方未定
	data: {
		...object <- ここだけ各APIから受け取る
	}
}
```

``` リスト
{
	response_id: uuid <- ログ追跡用のUUIDを付与したい 使い方未定
	data: {
		...object <- ここだけ各APIから受け取る
	}
	limit,
	offset,
	count: length,
}
```
