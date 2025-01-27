---
tags:
  - diary
---
> [!IMPORTANT]
> このテンプレート[[01_diary]]の内容（TODOやTimeline）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## NOTE
### 今日の学び
- 論理削除、物理削除の場合はHTTPステータス204を返すでも良さそう、特にデータを返す必要のない場合は204(not contents)を使う
- パッケージuuidの使い方
	- import { v7 as uuidv7 } from 'uuid'
	- あとは呼び出せばいい
```
    const uuid = uuidv7()
    const newQuest = await prisma.quest.create({
      data: {
        ...req.body,
        uuid, <- オブジェクトをスプレッド構文で展開した後に書く
      } as Prisma.QuestCreateInput,
    })
    return res.status(201).json(newQuest)
```

