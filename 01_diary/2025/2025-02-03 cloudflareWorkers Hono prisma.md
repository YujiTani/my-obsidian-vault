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

### Wishlist
やりたいことを書く
