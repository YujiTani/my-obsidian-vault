---
tags:
  - note
  - supabase
  - prisma
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note
## 接続に必要な情報
### .envファイル
```
DATABASE_URL="postgres://[DB-USER].[PROJECT-REF]:[PRISMA-PASSWORD]@aws-0-us-east-1.pooler.supabase.com:6543/postgres?pgbouncer=true"

# Used for Prisma Migrations (use session mode or direct connection)
DIRECT_URL="postgres://[DB-USER].[PROJECT-REF]:[PRISMA-PASSWORD]@aws-0-us-east-1.pooler.supabase.com:5432/postgres"
```
DB-USER … DB接続に使用するユーザー
PROJECT-REF … `supabase`のダッシュボード > `setting` > `General` > `General settings` > `Project ID`を使う
PRISMA-PASSWORD … Projectを作成した時に設定したProjectのパスワードを使用する

### schema.prismaファイル
```
generator client {
  provider = "prisma-client-js"
  binaryTargets = ["native", "darwin-arm64"] // Bunを使用する場合に必要
}

datasource db {
  provider  = "postgresql"
  url       = env("DATABASE_URL")
  directUrl = env("DIRECT_URL")
}
```

### 実行コマンド
パッケージインストール
```bash
bun install @prisma/client
```

`schema`を作成し`client`の`generate`と`migrate`を実行する
```bash
bunx prisma generate
bunx prisma migrate dev --name first_prisma_migration
```

以下のメッセージが表示されればOK
```
Already in sync, no schema change or pending migration was found.

✔ Generated Prisma Client (v6.3.1) to ./node_modules/@prisma/client in 15
5ms
```