---
tags:
  - note
  - git
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note
gitignoreを自動生成するために便利なコマンドラインツール「gitignore.io」を使う

```
curl -sL https://www.toptal.com/developers/gitignore/api/node > .gitignore
```
Node.jsプロジェクトの場合、上記のコマンドでNode.js用の.gitignoreを生成できる

複数の環境やフレームワークを組み合わせたい場合は、カンマで区切って指定できる
```
curl -sL https://www.toptal.com/developers/gitignore/api/node,macos,visualstudiocode > .gitignore
```

利用可能なテンプレートの一覧を確認したい場合は
```
curl -sL https://www.toptal.com/developers/gitignore/api/list
```

を実行することで確認できる

