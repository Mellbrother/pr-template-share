# git subtree を用いた pr テンプレートの共通化

## 概要

複数のリポジトリで PR テンプレートを共有する方法記載しました

ご興味のある方は試してみてください

## 手順

### テンプレを開発環境に取り入れる

1. PR のテンプレートを管理するリポジトリを作成する（template-share-repository と呼ぶ）
2. 開発用の repository を作成する（develop-repository と呼ぶ）
3. develop-repository にテンプレートを追加する（template1.md と呼ぶ）
4. develop-repository で`git remote add <任意の名前(ここではtemplate-share-repositoryとする)> <template-share-repositoryのgitパス>`を実行する
5. develop-repository で`git remote -v`を実行し、リポジトリ登録が完了しているか確認する
6. develop-repository で`git subtree add --prefix=.github/PULL_REQUEST_TEMPLATE template-share-repository main`を実行する
7. develop-repository の.github/PULL_REQUEST_TEMPLATE に template1 があることを確認する
8. develop-repository でブランチを切り、差分を PUSH する
9. github の画面で Compare & pull request、または New pull request を押下する(次の画面の Create pull request は押下しない)
10. URLにクエリパラメーター（`?template=template1.md`）を付与して Enter を押下する
11. Create pull request を押下する
12. テンプレが表示される（例：https://github.com/Mellbrother/pr-template-share/pull/5 ）

### クエリパラメータ追加を回避する（クエリパラメータを付与するのが面倒な人向け）

1. chrome の拡張機能の[Requestly](https://chrome.google.com/webstore/detail/mdnleldcmiljblolnjhpnblkcekpdkpa)を入れる（リダイレクトできれば他のものでも良いです）
2. `/https://github.com/[アカウント名]/([0-9a-zA-Z._/\-]+)/compare/([0-9a-zA-Z._/\-]+)/`を`https://github.com/[アカウント名]/$1/compare/$2?template=template1.md`にリダイレクトさせるように設定する（アカウント名は適宜変えてください）

※ リダイレクトを特定のリポジトリのみ適用したいなどあれば、正規表現の値を調整してください

## 注意点

- `git subtree add --prefix=.github/PULL_REQUEST_TEMPLATE template-share-repository main`実行時に、git の差分があると`fatal: working tree has modifications.  Cannot add.`というエラーが発生するので、commit/stash などでファイル差分をなくしておいてください
- PULL_REQUEST_TEMPLATE フォルダと pull_request_template.md は共存できないため、pull_request_template.md は追加しないでください（追加するとクエリパラメータをつけてもファイルが優先されます）
- template-shapre-repository 　に対する PUSH 権限が必要です（権限がない場合は、リポジトリを fork して、そのリポジトリを利用してください）
