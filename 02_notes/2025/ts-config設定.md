---
tags:
  - note
  - tsconfig
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## importルール整備
tsで開発してるときに、importにルールを追加する事でファイル間で書き方を統一することができる

使用する設定ファイルは下記2つ
```
ts-config.json
eslint.config.js
```

ts-configに以下設定を記述することで、チェック時の基準ディレクトリ設定とpathのalias設定を追加できる
```JSON: ts-config.json
"compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    },
    "baseUrl": ".", // モジュール解決にルートディレクトリを指定
  },
```

eslint.configの設定
import行を整備するためには、import順のルールの明確化,import文を統一するためのルールが必要になる
```typescript: eslint.config.js
import importAlias from 'eslint-plugin-import-alias'
import unusedImports from 'eslint-plugin-unused-imports'

export default [
    plugins: { // importしたプラグインの使用設定
		import: fixupPluginRules(_import),
	    'import-alias': importAlias,
		'unused-imports': unusedImports,
    },

    languageOptions: {
      parserOptions: {
        project: './tsconfig.json', // tsconfigの設定読み込み
      },
    },

rules: {
  // インポート関連の基本ルール
  'import/extensions': 'off',              // ファイル拡張子の記述を強制しない
  'import/prefer-default-export': 'off',   // デフォルトエクスポートを強制しない
  'unused-imports/no-unused-imports': 'error',  // 未使用のインポートはエラー

  // 3. インポート順序のルール
  'import/order': ['error', {
    groups: ['builtin', 'external', 'parent', 'sibling', 'index', 'object', 'type'],
    'newlines-between': 'always',    // グループ間に空行を強制
    alphabetize: { order: 'asc' }    // アルファベット順にソート
  }],

  // 4. TypeScript固有のインポートルール
  '@typescript-eslint/consistent-type-imports': ['error', {
    prefer: 'type-imports'    // import type を強制
  }],

  // 5. エイリアスインポートのルール: @を./srcにマッピング
  'import-alias/import-alias': ['error', {
    aliases: [{ alias: '@', matcher: './src' }],
  }],

  // 6. 制限付きインポートのルール: // 相対パスのインポートを警告
  'no-restricted-imports': ['warn', {
    patterns: ['./*', '../*']
  }]
}

]
```
