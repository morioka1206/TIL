GitやGitHubについて何となくの理解でやっていたので
いい機会だと思い、備忘録としてまとめておきます。



## Gitって何なの?
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1111652/55502dba-ce8b-21da-bd80-362583c31068.png)

Gitは一言で言うと**分散型のバージョンの管理システム**のことです。
分散型ではないバージョン管理システムには中央集中型のSubversionなどがあるようです。

**中央集中型**はリポジトリへの接続が必須ですが
**分散型**のバージョン管理システムは各々のマシン上にリポジトリを作成して開発を行うことができ、現在のチーム開発の主流になっています。

Gitでアプリケーションを管理するとそれぞれの開発段階でアプリケーションの内容をセーブポイントのように記録して、時系列に沿って管理してくれます。このセーブポイントは遡ることができます。

### リポジトリとは
**バージョン管理にとって管理されるファイルと履歴情報を保管する箱のようなもの**をリポジトリと言います。
リポジトリ下のファイルやディレクトリをバージョン管理の範囲として指定します。

リポジトリには**ローカルリポジトリ**と**リモートリポジトリ**の２種類があります。

#### ローカルリポジトリ
ローカルリポジトリとは自分のPC上（ローカル環境）に置くリポジトリのことです。
作成したリポジトリは自分のPCの中にあるため、ファイルやディレクトリを変更、修正したい際は好きなタイミングでできます。

#### リモートリポジトリ
リモートリポジトリとは、外部サーバ上に置くリポジトリのことです。作成した箱がインターネットの別の場所にも作られる感じです。リモートリポジトリを直接変更修正はせず、ローカルリポジトリの変更修正を同期して、反映させます。

リモートリポジトリは外部のサーバー上にあるので他の人に作成したコードを共有できたり、チーム開発をしやすくさせたりできます。


## GitHubって何なの？
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1111652/b76cf40b-a71f-bc20-be79-3b0ee83cd56a.png)

Git HubはGitの仕組みを利用して、簡単に複数人での開発ができるようにしてくれるWebサービスです。世界中の人々はコードなどを保存、公開しています。
Git Hubは基本的に無料で使うことができます。GitHubに作成されたリポジトリは基本的には公開することになりますが、指定したユーザーがアクセスできるプライベートリポジトリにすることも可能です。


[Git Hub](https://github.co.jp/)


## Gitのインストール
Macの場合はGitはすでにインストールされています。最新版にするにはbrewを使ってインストールします。

```
% brew install git
```
Windowsの場合はインストローラーをダウンロードします。
[ダウンロードページ](https://gitforwindows.org/)

## GitHubDesktop
GitHubDesktopはGitHubが提供しているデスクトップ用のアプリケーションです。
本来Gitはコンソールで作業しますが、GitHubDesktopはデスクトップ上で簡単にリモートリポジトリの作成やコミット、プルなどが簡単にできるツールです。

[GitHubDesktop](https://desktop.github.com/)
[ferret GitHub Desktop：初心者でも分かる、易しい使い方](https://ferret-plus.com/8498)

これを使うことで簡単にGitHubを扱うことができますが、今回は紹介に止めて
GUIしかできないのかとならないように基本のコマンドラインでの操作で行っていきます。

## Gitの初期設定
ターミナルで作業していきます。
Gitではソースコードの変更履歴を確認できますが、誰が変更をしたのかを確認するための情報が必要になります。識別するための情報としてユーザー名とメールアドレスを登録します。

```console:ユーザー名
% git config --global user.name ユーザー名
```

```console:メールアドレス
% git config --global user.email Eメールアドレス
```

```console:
% git config --list
```
と入力すると登録されている情報が確認できます。

## GitHubのアカウント作成
[GitHub](https://github.com/)へアクセスしてアカウントを作成してください。

[![Image from Gyazo](https://i.gyazo.com/a4889dcae459375893ea9bfc848b0cca.png)](https://gyazo.com/a4889dcae459375893ea9bfc848b0cca)

## リモートリポジトリの作成
[![Image from Gyazo](https://i.gyazo.com/e0b40ddfb41e2e2e25bd90e057050752.png)](https://gyazo.com/e0b40ddfb41e2e2e25bd90e057050752)

GitHubでリモートリポジトリを作成します。
左上の**Create Repository**をクリックしてください。

[![Image from Gyazo](https://i.gyazo.com/2f46412bf3eac48e729795301209bb08.png)](https://gyazo.com/2f46412bf3eac48e729795301209bb08)

リポジトリ作成画面に遷移しました。
リポジトリ名を任意のものを入力してください。
リポジトリの種類では公開したい場合は**Public**に非公開にしたいばいは**Private**を選択します。
Add a README fileを選択するとREADMEのファイルを作成してくれます。

入力できたら**Create repository**をクリックしてください。
リモートリポジトリが作成できました。





次回はローカルリポジトリを作成やGitのコマンドについてなどをまとめていきます。


>参考サイト
[【超入門】初心者のためのGitとGitHubの使い方](https://tech-blog.rakus.co.jp/entry/20200529/git)
[GitHub GITチートシート](https://training.github.com/downloads/ja/github-git-cheat-sheet.pdf)
[modis GitHubとは？使い方や知っておきたい知識を解説！
](https://www.modis.jp/staffing/insight/column_30/)




