---
tags:
  - note
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note

```
{
  // 公式にあるBunのベストプラクティス設定
  "compilerOptions": {
    // ----- 最新の機能を有効化するための設定 -----

    // 利用するライブラリを指定。ESNextの最新機能と、ブラウザ環境用のDOM機能を使用します。
    "lib": ["ESNext", "DOM"],
    // 出力されるJavaScriptのバージョンを指定。ESNextは最新のECMAScript機能を利用可能にします。
    "target": "ESNext",
    // 使用するモジュールシステムの指定。ESNextは最新のモジュール形式を使用します。
    "module": "ESNext",
    // モジュール検出方法を強制的に実施。モジュール間の依存関係を明確に管理します。
    "moduleDetection": "force",
    // JSXのトランスパイル方式を指定。Reactの新しいJSX変換方式を利用する設定です。
    "jsx": "react-jsx",
    // JavaScriptファイルも対象に含める。TypeScriptプロジェクト内でJSファイルを扱う場合に有効です。
    "allowJs": true,

    // ----- バンドラー向けの設定 -----
    // バンドラーに最適化されたモジュール解決方法を指定。最新のバンドラー仕様に合わせた動作をします。
    "moduleResolution": "bundler",
    // TypeScriptファイルの拡張子をインポート時に許可する設定です。
    "allowImportingTsExtensions": true,
    // モジュールのシンタックスをそのまま出力する設定。変換せずに元の記述を維持します。
    "verbatimModuleSyntax": true,
    // コンパイル時にファイルを出力しない設定。型チェックのためだけに使用される場合に便利です。
    "noEmit": true,

    // ----- ベストプラクティスに沿った設定 -----
    // 厳格な型チェックを有効にして、予期しないエラーを早期に検出します。
    "strict": true,
    // 外部ライブラリの型チェックを省略し、コンパイル速度を向上させます。
    "skipLibCheck": true,
    // switch文でのbreak等を明示せず、意図しない処理のフォールスルーを防ぎます。
    "noFallthroughCasesInSwitch": true,

    // ----- より厳密なチェック設定（デフォルトでは無効） -----
    // 使用されていないローカル変数をチェックします（現状は無効）。
    "noUnusedLocals": false,
    // 使用されていない関数パラメータをチェックします（現状は無効）。
    "noUnusedParameters": false,
    // インデックスシグネチャによるプロパティアクセスを禁止し、予期しないアクセスを防ぎます（現状は無効）。
    "noPropertyAccessFromIndexSignature": false
  },
  "include": ["src/**/*.ts", "src/**/*.tsx", "src/**/*.test.ts", "src/**/*.mts"]
}
```