---
tags:
  - note
  - prisma
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note

# prismaのseed作成方法

`/prisma/seed.ts`を作成する
```
import { Prisma, PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

const questData: Prisma.QuestCreateInput[] = [...Array(100)].map((_, i) => ({
  name: `Quest${i + 1}`,
  description: `Quest${i + 1} description`,
  state: "DRAFT",
}));

const main = async () => {
  const result = await prisma.quest.createMany({
    data: questData,
    skipDuplicates: true,
  });
  console.log({ result });
};

main()
  .catch((e) => {
    console.error(e);
    process.exit(1);
  })
  .finally(async () => {
    await prisma.$disconnect();
  });

```

package.jsonに追記
下記の記述をすることで`npx prisma db seed`実行時に、コマンドを読み込んでくれる別途`tsx`や`ts-node`のインストールが必要
```
,
  "prisma": {
    "seed": "tsx prisma/seed.ts"
  }
}
```