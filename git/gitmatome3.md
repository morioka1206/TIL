
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1111652/c53644f9-468e-d165-ab70-5c1245a8d9d7.png)


前回はGitHubの基本的な用語、ローカルリポジトリの作成まで行いました。
次はGitを利用する上で重要なブランチをまとめておきます。

- [初心者向け GitとGitHubについて①](https://qiita.com/morioka1206/items/713ffaeff8d7075ba3b4)
- [初心者向け GitとGitHubについて②](https://qiita.com/morioka1206/items/926acec8642cefa1fcc5)


## ブランチとは
ブランチとはリポジトリで管理しているファイルやディレクトリの変更の流れ、コミットの連なりです。リポジトリは必ずブランチを持っています。

アプリケーションの開発では複数の新たな機能追加やバグ修正などを並行して行うことがあります。
その作業ごとに分岐して管理することができれば、チーム開発でも同じファイルを同時に編集することができるようになります。

大元のブランチを**masterブランチ**、分岐したブランチを**トピックブランチ**といいます。
大元のブランチからブランチを分岐させることを「**ブランチを切る**」といいます。

作業が完了した分岐したブランチをマージ(結合)することでまた一つのブランチに戻すことができます。

#### ブランチのメリット
- ブランチを切ることで目的別に同時並行で作業が行えること
- 不具合が発生した場合も対応が容易になること
- 他のメンバーの作業による影響を受けることなく、自分の作業に取り組める

## ブランチの作成
```console:現在のブランチ一覧
% git branch
```

`git branch`と入力すると現在のブランチ一覧が表示されます。
作業中のブランチには「*」が付きます。

```console:
* master
```

それではブランチを作成しましょう。

```console:ブランチを作成
% git branch　ブランチ名
```
作成したブランチへの移動は`checkoutコマンド`でできます。

```console:ブランチへ移動
% git checout ブランチ名
```

移動できると`Switched to branch 'ブランチ名'`と表示されます。
またブランチの作成と移動を同時に行う場合は`git checkout -b ブランチ名`でできます。

```console:ブランチの作成と移動
% git checkout -b ブランチ名
```

## ブランチにプッシュ
まずは`addコマンド`でインデックスへ追加します。

```console:インデックスへ登録
% git add 追加したいファイル
```

コミットします。

```console:ローカルリポジトリへコミット
% git commit -m "コメント"
```

リモートリポジトリへ反映させます。
ブランチ名を指定するだけでプッシュすることができます。

```console:ブランチにプッシュ
% git push origin ブランチ名
```

[![Image from Gyazo](https://i.gyazo.com/b2914c62edb91d6368cb5ee1a373fcca.png)](https://gyazo.com/b2914c62edb91d6368cb5ee1a373fcca)

一つだったブランチが2つになりました。

## masterブランチへのマージ
新機能の追加などが完了し、メインのmasterブランチに取り込むことになったとします。
通常はプルリクエスト、コードレビューなどがあると思いますが、それも終わったということにします。

ブランチに取り込むことを**マージ**といいます。
まずは作業中のブランチをmasterブランチに切り替えます。

```console:ブランチをmasterにする
% git checkout master
```

次にマージしたいブランチをマージする`git mergeコマンド`を入力します。

```console:ブランチをマージする
% git merge ブランチ名
```

次にGitHubへプッシュします。

```console:GitHubへプッシュ
% git push origin master
```

これでmasterブランチへのマージができます。


## ブランチからプルする
他の開発者がトピックブランチで作業するとします。
その場合はそのブランチに`checkoutコマンド`で移動して`pullコマンド`を入力することで可能になります、

```ブランチに移動する
% git checkout ブランチ名
```

次にリモートブランチのコードを`pullコマンド`で取得します。

```console:リモートブランチからコードを取得
% git pull
```

## ブランチの削除
使わなくなったブランチは削除することができます。

```console:ブランチの削除
% git branch -d ブランチ名
```

`git branch`コマンドで削除されているか確認しましょう。







>参考サイト
[【超入門】初心者のためのGitとGitHubの使い方](https://tech-blog.rakus.co.jp/entry/20200529/git)
[GitHub GITチートシート](https://training.github.com/downloads/ja/github-git-cheat-sheet.pdf)
[modis GitHubとは？使い方や知っておきたい知識を解説！
](https://www.modis.jp/staffing/insight/column_30/)[Gitではじめるバージョン管理 〜ローカルリポジトリでファイルを管理してみよう〜](https://www.hivelocity.co.jp/blog/34777/)
[TechAcademyマガジン 今さら聞けない！GitHubの使い方【超初心者向け】](https://techacademy.jp/magazine/6235)




