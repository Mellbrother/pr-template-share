# サブツリーを用いた pr テンプレートの共通化

## 手順

### テンプレを開発環境に取り入れる

1. PR のテンプレートを管理するリポジトリを作成する（template-share-repository と呼ぶ）
2. 開発用の repository を作成する（develop-repository と呼ぶ）
3. develop-repository にテンプレートを追加する（template1.md と呼ぶ）
4. develop-repository で`git remote add <任意の名前(ここではtemplate-share-repositoryとする)> <template-share-repositoryのgitパス>`を実行する
5. develop-repository で`git remote -v`を実行し、リポジトリ登録が完了しているか確認する
6. develop-repository で`git subtree add --prefix=.github/PULL_REQUEST_TEMPLATE template-share-repository main`を実行する
7. develop-repository の.github/PULL_REQUEST_TEMPLATE に template1 があることを確認する
8. develop-repository で PR を作成する

### クエリパラメータ追加を回避する

1. chrome の拡張機能の[Requestly](https://chrome.google.com/webstore/detail/mdnleldcmiljblolnjhpnblkcekpdkpa)を入れる（リダイレクトできれば他のものでも良いです）
2. `/https://github.com/[アカウント名]/([0-9a-zA-Z.-_/]+)/compare/([0-9a-zA-Z.-_/]+)...([0-9a-zA-Z.-_/]+)/`を`https://github.com/[アカウント名]/$1/compare/$2...$3?template=template1.md`にリダイレクトさせるように設定する（アカウント名は適宜変えてください）

## 注意点

- `git subtree add --prefix=.github/PULL_REQUEST_TEMPLATE template-share-repository main`実行時に、git の差分があると`fatal: working tree has modifications.  Cannot add.`というエラーが発生するので、commit/stash などでファイル差分をなくしておいてください
