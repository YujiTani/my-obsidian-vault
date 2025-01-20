---
tags:
  - note
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## NOTE

prismaでmigration devを実行した際に、下記エラーが発生
どうやらmigrationを実行するために、一時的なデータベース(shadow database)を作りたいのだが指定しているユーザーにDB作成権限がないためエラーが発生しているようだ。

```
Prisma Migrate could not create the shadow database. Please make sure the database user has permission to create databases. Read more about the shadow database (and workarounds) at https://pris.ly/d/migrate-shadow

Original error: 
ERROR: permission denied to create database
   0: schema_core::state::DevDiagnostic
             at schema-engine/core/src/state.rs:276
```

以下のどちらかの方法で権限を追加する
- 既存ユーザーへの追加
```
ALTER USER or ROLE 'username' CREATEDB;
```

- 新しいユーザーを作成し、権限を付与
```
CREATE USER or ROLE 'username' WITH PASWORD 'password' CREATEDB;
```

