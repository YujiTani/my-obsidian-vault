---
tags:
  - note
  - JWT
  - Auth
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note 
# トークンベースの認証システムの流れ
新規登録
1. [ ] ユーザーIDとパスワードをバックエンドに渡します。
	1. [ ] リクエストバリデーション
	2. [ ] 既存ユーザーでないか確認
	3. [ ] パスワードをハッシュ化する
	4. [ ] DBに保存
	5. [ ] JWT生成
2. [ ] ログインができれば認証し、クライアントにJWTを返します
3. [ ] トークンをCookieに保存する
4. [ ] APIを叩く際にJWTを含めてリクエストする。
	1. [ ] トークンのすべての要素に対して検証を行う
	2. [ ] 問題があれば、無効なトークンだとメッセージを返す
	3. [ ] 問題なければ、有効期限をリフレッシュする
	4. [ ] リフレッシュしたトークンをクライアントに返す

## 留意点
7. httpsを必ず使う
8. 暗号化アルゴリズムをnone（署名なし）にしない
9. トークンのライフサイクルをできるだけ適切にしてリフレッシュする

## 参考記事
[JSON Web Token（JWT）の仕様と実装例を紹介 | 株式会社LIG(リグ)｜DX支援・システム開発・Web制作](https://liginc.co.jp/617624)

## JWTの作り方
JWTは次の３つからなる
『ヘッダ』『ペイロード』『署名』
それぞれを連ねて.で繋いだ状態がJWTと呼ばれる
![[スクリーンショット 2025-02-11 14.02.11.png]]

### ヘッダとペイロードを作る
10. ヘッダはほぼ固定のJSONを使い、`base64URL`という方式でエンコードされる
bashを使って作成する場合、以下のようなコマンドになる
```
echo -n '{ "alg": "HS256", "typ": "JWT" }' | base64 | tr '+/' '-_'
```

11. ペイロードには、サービス独自のユーザー情報などが入る
```
echo -n '{  
	"sub": "user123", // ユーザーの一意な識別子
	"name": "User Name", // ユーザー名
	"iat": 1671596066, // トークンの発行時刻
	"exp": 1671599666, // トークンの有効期限
	"role": "user", // ユーザーの役割
}' | base64 | tr '+/' '-_' 
```

1と2で作ったJSONをbase64URL形式でエンコードしたものを`.`で繋ぎ合わせることでJWTの前半部分ができます。
```
(echo -n '{ "alg": "HS256", "typ": "JWT" }' | base64 | tr '+/' '-_').(echo -n '{  
	"sub": "user123", // ユーザーの一意な識別子
	"name": "User Name", // ユーザー名
	"iat": 1671596066, // トークンの発行時刻
	"exp": 1671599666, // トークンの有効期限
	"role": "user", // ユーザーの役割
}' | base64 | tr '+/' '-_' )
```


### なぜエンコードに`base64URL`を使うのか？
- base64はテキストデータやバイナリデータを、ASCII 文字列に変換するエンコードしたり、デコードしたりできるコマンド
- `base64URL`は`base64`をURLなどでもセーフに使えるようにしたエンコード方法で、具体的にはURL内で異なる意味を持つ`+`や`/`を`-`と`_`に置き換える
- ASCII 文字列は、1960年に標準化された基本的な文字コードです。国際的な基準となっているため、インターネットの通信で広く使用されています

## 署名を作る
署名はASCII文字列に変換されたヘッダー&ペイロードと、独自生成した秘密鍵をあわせた状態で、指定の暗号化アルゴリズムで暗号化する。
暗号化されるとバリナリデータとなるため、さらにそれをbase64URL方式でエンコードする。

## JWTトークンを生成する
作成したヘッダ、ペイロード、署名をペイロードでつなぎ合わせたものをJWTという