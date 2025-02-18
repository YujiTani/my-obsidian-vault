---
tags:
  - note
  - git
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note

特定のブランチ以外を削除
```
git branch -d $(git branch | grep -v "main")
```
-vは以外を除外するオプション
-dを-Dにするとマージしてないブランチも強制削除