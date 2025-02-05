---
tags:
  - note
  - TypeScript
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note

ファイル解析がうまくいってない場合のエラー

エラー例:
```
Parsing error: ESLint was configured to run on using `parserOptions.project`
However, that TSConfig does not include this file. Either:
```

解決方法:
1. コンパイルやLintチェックが必要なファイルか判断し、チェックから外す or チェックを通す方法を調べる

チェックを外す方法まとめ
word単位, 行単位, ファイル単位など
[TypeScript と ESLint における検査エラーを無視したい時のおまじないまとめ | blog.ojisan.io](https://blog.ojisan.io/eslint-ts-ignore/)

`eslint.config.mjs`で除外設定する
以下でファイルを指定する
```

export default {
    {
        ignores: ['dist'],
    }
}
```