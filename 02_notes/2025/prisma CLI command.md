---
tags:
  - note
  - prisma
  - CLI
  - command
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

prismaCLIで使えるcommand
## note

| command                                          | 説明                                             |
| ------------------------------------------------ | ---------------------------------------------- |
| npx prisma init --datasource-provider postgresql | 実行ディレクトリに必要最低限​​のファイルを含むディレクトリを作成、shema.prisma |
| npx prisma generate                              | schema.prismaファイルを読み込んで、Prisma クライアントを生成する     |
| npx prisma generate --watch                      | schema.prismaの変更を監視して、都度Prisma クライアントを再生成する    |
| npx prisma validate                              | schemaファイルの構文が正しいかチェックする                       |
| npx prisma validate --schema {path}              | shcemaファイルを指定して、構文チェックする                       |
| npx prisma db pull                               | 既存のDBからschemaファイルを作成する                         |
| npx prisma db pull --print<br>                   | schemaファイルを変更せずに、作成内容をターミナルに表示                 |
|                                                  |                                                |
