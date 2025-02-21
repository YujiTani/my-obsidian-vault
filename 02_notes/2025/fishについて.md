---
tags:
  - note
  - shell
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note
まっさんがzshで実装した内容がfishの初期からついてそうだなと思ったのでメモ残しておきます

# fish（Friendly Interactive SHell)

## あいまい検索でディレクトリ移動
z というプラグインを入れると、ディレクトリ構成を無視した移動ができる

## aliasコマンド
追加したalias Listがみれる
```
alias dcb 'docker compose build'
alias dcbpp 'docker compose build --progress=plain'
alias dcd 'docker compose down'
alias dcdv 'docker compose down -v'
alias dce 'docker compose exec'
alias dcl 'docker compose logs'
alias dclc 'docker compose logs | pbcopy'
alias dcp 'docker compose ps'
alias dcpa 'docker compose ps -a'
alias dcu 'docker compose up'
alias dcud 'docker compose up -d'
alias g git
alias ga 'git add'
alias gb 'git branch'
alias gc 'git commit'
alias gco 'git checkout'
alias gp 'git push'
alias nv nvim
```

## 自動補完機能

## シンタックスハイライト
## 関数定義
bashやzshとけっこう書き方が違うので注意
```sh
function fish_greeting
    echo "Welcome to fish!"
end
```

## 変数定義
```sh
set -gx PATH $PATH /additional/path # path
set name value #locak
```

## 設定をブラウザで確認できる
下記コマンド実行
```sh
fish_config
```