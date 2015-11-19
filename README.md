
# pull request の練習リポジトリ

GithubのREADMEファイルはGithubマークダウン記法を使って記述する。

[markdownで行こう！](https://gist.github.com/wate/7072365)

## おすすめのGithub拡張機能
+ [octotree](https://github.com/buunguyen/octotree)
    + Github上にフォルダtreeを表示
+ [Zenhub](http://qiita.com/GeckoTang/items/f75b9a1c20c8e5091147)
    + Githubにカンバンなどの機能追加

## gitコマンドまとめ
| コマンド        | 意味　          |
| --------------- | --------------- |
| git init | カレントディレクトリを Git リポジトリに変換する |
| git status | 作業ディレクトリやステージングエリアの状況を確認する |
| git log | コミット履歴の一覧表示。 |
| git log --oneline | logの出力結果を一行にまとめる |
| git log -n 件数 | 表示する件数を絞る |
| git add ファイル名 | 作業ディレクトリ内の変更をステージングエリアに追加する |
| git commit -m "コメント" | ステージされた内容をローカルリポジトリにコミットする |
| git remote add origin リポジトリURL | Github上のリポジトリとの接続の作成 |
| git push -u origin ブランチ名 | ブランチをローカルリポジトリからリモートリポジトリに送る操作 |
| git pull origin ブランチ名 | 最新のリモートリポジトリを現在のローカルリポジトリにマージ |
| git branch | 現在のブランチの情報を表示 |
| git checkout ブランチ名 | ブランチを移動する |
| git checkout -b ブランチ名 | 新規ブランチの作成 |
| git checkout -d ブランチ名 | ブランチの削除 |
| git checkout コミットハッシュ | 指定したコミットまでコードを逆上る |
| git checkout ブランチ名 | 最新のコミットまでコードを戻す |
| git commit --amend -m "新規コメント" | ひとつ前のコミットのコメントを修正する |
| git cherry-pick コミットハッシュ | 別ブランチのコミットをマージする |
| git clone リポジトリURL | リモートリポジトリを複製する |

## git -> Githubへのpushの流れ
1. ローカル上でディレクトリ作成(プロジェクト)
2. ディレクトリ内でgit init コマンドを使い初期化
3. 何かしらの作成 or 編集
4. git add ファイル名コマンドで更新したものをステージングエリアに上げる
5. git commit -m "コメント"コマンドで変更を保存する
6. Github上でリモートリポジトリを作成
7. git remote add と git pushのコマンドをコピー
8. git remote add origin githubのURLコマンドでローカルとリモートを接続
9. git push -u origin masterコマンドで保存したソースコードをリモートへ送る

## Github -> gitへのpullの流れ
1. リモートリポジトリをローカルより育てる
2. `git pull origin master` コマンドでリモート上の最新リポジトリをローカルに持ってくる

## Pull Requestの流れ
1. `git checkout -b ブランチ名` コマンドで新規ブランチを作成 (同時にブランチの切り替えも行ってくれる)
2. 何かしらのアップデートをする
3. `git add .`、`git commit -m "コメント"`の順で保存する
4. `git push origin 新しいブランチ名` コマンドでリモート上に新しくブランチを作成してpush
5. Github上でpull requestを送る
6. 管理者がrequestをレビューする
7. 問題があれば差し戻す (コメントを自由に付けられる)
8. 再度問題を修正し、`add`、`commit`、`push`で修正内容をpull reqに上乗せして送る
    + pull req中に同じブランチに修正内容をpushすると、それだけで修正内容がpull reqにのっかる
9. 修正内容を確認し、mergeする
10. ブランチを削除する

## ブランチの切り替え方
+ `git checkout ブランチ名` コマンドでブランチを行き来できる
    + 現在いるブランチ上で何かしらの変更を行っていた場合はその変更内容を保存もしくは削除してからブランチを移動すること

## commitコメントの修正
+ `git commit --amend -m "新規コメント"` コマンドで編集可能

## 指定したコミットまでコードを逆上る方法
1. Github上 (もしくはlog上) でコミットのハッシュをコピー
2. `git checkout ハッシュ` コマンドで指定したコミットまで戻る
3. `git checkout ブランチ名` コマンドで最新のコミットに戻る

## 別ブランチのコミットをmasterブランチへ追加する方法
1. 別ブランチでの変更をcommitしきる
2. `git log --oneline`でコミットのハッシュを見る
3. `git checkout master`でmasterブランチへ移動
4. `git cherry-pick ハッシュ`で別ブランチのコミットをmasterへ追加

## ローカルブランチの削除
+ `git branch -d ブランチ名`
+ もし`error: The branch 'ブランチ名' is not fully merged.`がでれば、
    + `git branch -D ブランチ名`で強制削除も可能
