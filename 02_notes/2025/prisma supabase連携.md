---
tags:
  - note
  - prisma
  - supabase
  - Hono
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note
# Honoを使ってPrismaとSupabaseを連携
## 作業フロー
1. Honoプロダクト作成
2. SupaBaseにプロダクト、DBを作成
3. DBを操作するユーザーを作成
4. Prismaをインストール
5. Prismaを初期化
6. .env(環境変数設定)をprismaに読み込ませる設定を書く
7. Prismaスキーマを作成
8. prisma migrateを実行する

## 詳細(一部のみ抜粋)
### 1. Honoプロダクト作成
Bunを使ってみた

brew install
```
brew install oven-sh/bun/bun
```

honoプロダクト作成
```
bun create hono@latest my-app
```

```
cd my-app
bun install
```

```
bun run dev
```

test
```
bun test index.test.ts
```

---

### DBを操作するユーザーを作成
supabaseのSQLエディターを使う
```
-- Create custom user
create user "prisma" with password 'custom_password' bypassrls createdb;

-- extend prisma's privileges to postgres (necessary to view changes in Dashboard)
grant "prisma" to "postgres";

-- Grant it necessary permissions over the relevant schemas (public)
grant usage on schema public to prisma;
grant create on schema public to prisma;
grant all on all tables in schema public to prisma;
grant all on all routines in schema public to prisma;
grant all on all sequences in schema public to prisma;
alter default privileges for role postgres in schema public grant all on tables to prisma;
alter default privileges for role postgres in schema public grant all on routines to prisma;
alter default privileges for role postgres in schema public grant all on sequences to prisma;

```

password設定
パスワード生成ツール仕様を推奨
```
-- alter prisma password if needed
alter user "prisma" with password 'new_password';

```

---
### .env(環境変数設定)をprismaに読み込ませる設定を書く
supabase内のヘッダーにconnectと書かれてる場所があるので、それを使う

schema.prismaにも設定を追加
```
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider  = "postgresql"
  url       = env("DATABASE_URL")
  directUrl = env("DIRECT_URL")
}
```

Seedも作っておこう
[[prisma seed作成方法]]