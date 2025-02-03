---
tags:
  - diary
  - Hono
  - prisma
---
# TITLE
## きょうやることのメインタスク名

## TODO(今日やること)
- [ ] HonoAPI開発
	- [ ] RPC設定できるようになる
	- [ ] CFWでPrismaを使えるようにアダプター設定をする
	- [ ] supabaseを使って見るように変更
- [ ] TODO2
## NOTE
### TODOの振り返り(成果について、それはなぜか)



### MEMO
メモしたいことを書く

PrismaはNode.js環境で動作することを想定されているため、CFW環境では、動作できない。
そのためHonoのDriver Adaptersという機能を使う必要がある

```prisma.shemesに追加
previewFeatures = ["driverAdapters"] # ← 追加
}
```

client更新
```
npx prisma generate
```


``` package-install
bun add pg @prisma/adapter-pg
bun add -D @types/pg
```

[[prisma seed作成方法]]

参考記事
[Cloudflare Workers + Hono + Prismaでローカル環境構築](https://zenn.dev/slowhand/articles/30c6bc9fd418ab)

### [[prisma supabase連携]]
---
まずはユーザーを作成する

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
専用ユーザー "prisma" の作成:
特別なパスワードと権限（RLS を回避、データベース作成権限）を持つユーザーを作成します。

ロールの継承設定:
"postgres" ユーザーに "prisma" ロールの権限を与えることで、データベース管理ツール（Dashboard）での表示や変更確認を容易にしています。

スキーマ「public」への広範な権限付与:
既存のオブジェクト（テーブル、ルーチン、シーケンス）に対して完全なアクセス権限を "prisma" ユーザーに与えます。

また、将来的に "postgres" が作成する新規オブジェクトにも自動で同様の権限が付与されるようにデフォルト権限を調整します。

この設定により、Prisma といったツールがデータベースの変更を適切に反映・管理できるようになり、開発や運用上の利便性が向上します。

### Wishlist
やりたいことを書く
