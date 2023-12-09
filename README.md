# サブツリーを用いた pr テンプレートの共通化

## 手順

1. PR のテンプレートを管理するリポジトリを作成する（template-share-repository と呼ぶ）
2. 開発用の repository を作成する（develop-repository と呼ぶ）
3. develop-repository で`git remote add <任意の名前(ここではtemplate-share-repositoryとする)> <template-share-repositoryのgitパス>`を実行する
4. develop-repository で`git remote -v`を実行し、リポジトリ登録が完了しているか確認する
5. develop-repository で`git subtree add --prefix=.github/PULL_REQUEST_TEMPLATE template-share-repository main`を実行する
