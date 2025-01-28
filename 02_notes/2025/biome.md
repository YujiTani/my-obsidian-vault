---
tags:
  - note
  - biome
  - formatter
  - linter
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note
導入
```
npm install --save-dev --save-exact @biomejs/biome
```

### 初期設定ファイル作成
```
 npx @biomejs/biome init

Welcome to Biome! Let's get you started...

Files created 

  - biome.json
    Your project configuration. See https://biomejs.dev/reference/configuration

Next Steps 

  1. Setup an editor extension
     Get live errors as you type and format when you save.
     Learn more at https://biomejs.dev/guides/integrate-in-editor/

  2. Try a command
     biome check  checks formatting, import sorting, and lint rules.
     biome --help displays the available commands.

  3. Migrate from ESLint and Prettier
     biome migrate eslint   migrates your ESLint configuration to Biome.
     biome migrate prettier migrates your Prettier configuration to Biome.

  4. Read the documentation
     Find guides and documentation at https://biomejs.dev/guides/getting-started/

  5. Get involved with the community
     Ask questions and contribute on GitHub: https://github.com/biomejs/biome
     Seek for help on Discord: https://biomejs.dev/chat
```

### biome.json
```
{
	"$schema": "https://biomejs.dev/schemas/1.9.4/schema.json",
	"vcs": {
		"enabled": true,
		"clientKind": "git",
		"useIgnoreFile": true,
		"defaultBranch": "main"
	},
	"files": {
		"ignoreUnknown": false,
		"ignore": [
			"**/node_modules/**",
			"./tsconfig.json",
			"./package.json",
			"vite.config.ts"
		]
	},
	"formatter": {
		"include": [
			"src/**/*.js",
			"src/**/*.jsx",
			"src/**/*.ts",
			"src/**/*.tsx"
		],
		"enabled": true,
		"formatWithErrors": false,
		"attributePosition": "auto",
		"indentStyle": "tab",
		"indentWidth": 2,
		"lineWidth": 120
	},
	"organizeImports": {
		"enabled": true
	},
	"linter": {
		"enabled": true,
		"rules": {
			"recommended": true,
			"style": {
				"noNonNullAssertion": "off"
			},
			"suspicious": {
				"noExplicitAny": "warn"
			}
		}
	},
	"javascript": {
		"formatter": {
			"arrowParentheses": "always",
			"bracketSameLine": false,
			"bracketSpacing": true,
			"jsxQuoteStyle": "double",
			"quoteProperties": "asNeeded",
			"semicolons": "always",
			"trailingCommas": "all"
		}
	},
	"json": {
    "formatter": {
			"trailingCommas": "none"
		}
	}
}

```

### 発生したエラー
自分がtypescriptまだ理解が低いので、any方を完全に除外できなそうなのでruleを変更する

*エラー内容*
```
npm run check

> vite-express-project@0.0.0 check
> biome check --write ./src

./src/server/controllers/helper.ts:21:42 lint/suspicious/noExplicitAny ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ✖ Unexpected any. Specify a different type.
  
    19 │  * @param res レスポンス
    20 │  */
  > 21 │ export const handlePrismaError = (error: any, res: Response) => {
       │                                          ^^^
    22 │        if (error instanceof Prisma.PrismaClientKnownRequestError) {
    23 │                switch (error.code) {
  
  ℹ any disables many type checking rules. Its use should be avoided.
```

### 確認したrule
[noExplicitAny | Biome](https://biomejs.dev/linter/rules/no-explicit-any/) 公式
lintプロパティのsuspiciousに追加

![[スクリーンショット 2025-01-28 23.59.50.png]]

```
	"linter": {
		"enabled": true,
		"rules": {
			"recommended": true,
			"style": {
				"noNonNullAssertion": "off"
			},
			"suspicious": {
				"noExplicitAny": "warn" ← ここで警告レベルに変更
			}
		}
	},
```