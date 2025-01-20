---
tags:
  - note
  - prisma
  - DB
  - postgresql
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note
Prismaを使うためには、ユーザーに必要な権限を与える必要があります。

### これらの権限が必要な理由：
- マイグレーション操作のため
	- テーブルの作成/変更/削除
	- インデックスの作成
	- 外部キーの設定
	- データ操作のため
	- レコードの追加/更新/削除

- データ操作のため
	- データの検索/取得

- Prisma固有の機能のため:
	- マイグレーション履歴の管理
	- スキーマの同期確認

これらの権限がないと、prisma関連のコマンドが正常に動作しない。

## 権限付与の方法
いくつか方法が存在する
1. スーパーユーザー権限を付与する
簡単だが、本番環境などでは推奨しない
```
ALTER USER 'username' WITH SUPERUSER;
```

2. 必要な権限をまとめて付与
```
# -- publicスキーマの指定ユーザーに、スキーマオブジェクトで使えるすべての権限を付与
GRANT ALL ON SCHEMA public TO 'username';

# -- すべてのテーブルに対する権限をpublicスキーマの指定ユーザーに付与
GRANT ALL ON ALL TABLES IN SCHEMA public TO 'username';

# -- 将来作成されるすべてのテーブルに対する権限を自動付与
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL ON TABLES TO 'username';
```
コマンド解説
`GRANT ALL ON SCHEMA`...これで一つの意味となるスキーマオブジェクトで使える(`ON SCHEMA`)すべての権限を付与(`GRANT ALL`)

`


postgresのスキーマの構造図
```
Database
└── Schema (public) ──────────── GRANT ALL ON SCHEMA public
    └── オブジェクト群 ───────── GRANT ALL ON ALL TABLES IN SCHEMA public
        ├── Tables            GRANT ALL ON ALL SEQUENCES IN SCHEMA public
        ├── Sequences         GRANT ALL ON ALL FUNCTIONS IN SCHEMA public
        └── Functions
```


### 構文パターンの使い分け

1. **スキーマレベルの権限**:
```sql
GRANT [権限] ON SCHEMA [スキーマ名] TO [ユーザー名];
```

2. **スキーマ内のオブジェクトへの権限**:
```sql
GRANT [権限] ON ALL [オブジェクトタイプ] IN SCHEMA [スキーマ名] TO [ユーザー名];
```

3. **新規作成オブジェクトのデフォルト権限**:
```
ALTER DEFAULT PRIVILEGES IN SCHEMA [スキーマ名]
GRANT [権限] ON [オブジェクトタイプ] TO [ユーザー名];
```

[[付与されている権限の確認方法]]