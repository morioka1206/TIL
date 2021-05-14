![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1111652/d72ef381-169e-adcb-8008-71a70852562b.png)


# Gitのフォークとクローン
GitHubについて調べていると**clone**以外に**fork**という機能があることを知りました。
どうやらフォークとクローンは似ているみたいなのでイラストを使いながらまとめてみることにします。


#### 対象読者
- ひとりで勉強している初学者

GitHubを用いてチーム開発をしている方は対象にしていません。
チーム開発でのクローン、フォークについては別の機会に。



## Gitのforkとcloneの違い
GitHub Docsの用語集にフォークとクローンについて説明がありましたので引用します。

#### フォーク
> フォークとは、個人が別のユーザのリポジトリをコピーしたものであり、その個人のアカウントに存在します。フォークであれば、元の上流リポジトリに影響を与えることなしに、プロジェクトに対して自由に変更を加えることができます。また、いずれのリポジトリも接続は切れていないので、上流リポジトリでプルリクエストをオープンしてフォークと最新の変更とが常に同期されるようにすることもできます。

#### クローン
> クローンとは、コンピュータ上に存在するリポジトリのコピーです。ウェブサイトのサーバ上のどこかにあるのではなく、またそのコピーを作成する動作とも異なります。クローンを作成すると、お気に入りのエディタでファイルを編集できるようになり、オンラインになっていなくても Git を使用して変更を追跡できます。クローン作成元のリポジトリもリモートバージョンへの接続が切れることはないので、オンラインになればローカルでの変更をリモートにプッシュすることで同期が取れます。

どちらもコピーのことと書いてあります。

ちょっとよくわからないですよね。わかりやすくしてみます。

### フォークとは
フォークとは他人のユーザーのリポジトリをコピーして、自分のアカウントのリポジトリとしてコピーすることです。これにより、他人のユーザーのリポジトリに影響を受けずに、自由に変更を加えることができます。

[![Image from Gyazo](https://i.gyazo.com/3ec83cfec42d03de6e11bccb3bcdab22.png)](https://gyazo.com/3ec83cfec42d03de6e11bccb3bcdab22)


### クローンとは
クローンは単にリモートリポジトリを自分のローカルリポジトリに複製することです。あくまで自分のリモートリポジトリのものではないので、権限がなければ変更を加えることはできません。

[![Image from Gyazo](https://i.gyazo.com/cf67740d5eaae75e913ac47c824e7eee.png)](https://gyazo.com/cf67740d5eaae75e913ac47c824e7eee)

### フォークの使い道
フォークは主な目的としては**フォークしたユーザーのリポジトリへの変更を提案したり、そのリポジトリから自分のアイデアの出発点として活用するため**に使えます。

＊無気力人間をやる気マックス人間に変えてみた。

[![Image from Gyazo](https://i.gyazo.com/fc987937ae71a16f6f8d0b7787d27d95.png)](https://gyazo.com/fc987937ae71a16f6f8d0b7787d27d95)

### クローンの使い道

[![Image from Gyazo](https://i.gyazo.com/cf67740d5eaae75e913ac47c824e7eee.png)](https://gyazo.com/cf67740d5eaae75e913ac47c824e7eee)

クローンの主な目的としては、**好きなVSコードなどのエディタでソースコードを見たり、ローカルサーバーで実際にアプリケーションを動作させてみたりすること**ができます。

# クローンのやり方、フォークのやり方
GitHub Desktopからやるやり方もありますが、一般的なGitHubページからフォーク、クローンする方法を説明します。

どこか適当な他人のGitHubのページにアクセスしてください。

## フォークのやり方

[![Image from Gyazo](https://i.gyazo.com/b57bddcd61a30abf07c73b19ec3dad68.png)](https://gyazo.com/b57bddcd61a30abf07c73b19ec3dad68)

GitHubのページの右上に**Fork**とあります。クリックしましょう。
[![Image from Gyazo](https://i.gyazo.com/0d3f101c80eab920df451bcf3b95cd21.png)](https://gyazo.com/0d3f101c80eab920df451bcf3b95cd21)

すると自分のGitHubアカウント名が表示されます。アカウント名をクリックします。

[![Image from Gyazo](https://i.gyazo.com/9aae058f16a2f42962ec4ff725fb1eab.png)](https://gyazo.com/9aae058f16a2f42962ec4ff725fb1eab)

自分のアカウントにslackのリポジトリが作成されています。
これだけで自分のアカウントにコピーすることができました。

## クローンのやり方

[![Image from Gyazo](https://i.gyazo.com/139a0426046dd096a4b8bdcc9bc14376.png)](https://gyazo.com/139a0426046dd096a4b8bdcc9bc14376)

**Code**をクリックします。

[![Image from Gyazo](https://i.gyazo.com/4e7b14c569f0983a79721b0292a5d247.png)](https://gyazo.com/4e7b14c569f0983a79721b0292a5d247)

クローンの方法についての選択画面が表示されます。
今回は一般的なHTTPSを使ってクローンしましょう。

[![Image from Gyazo](https://i.gyazo.com/a66867c80007aa56c8c3263c0e0a20fc.png)](https://gyazo.com/a66867c80007aa56c8c3263c0e0a20fc)

クリップのアイコンをクリックすることでコードがコピーできます。

[![Image from Gyazo](https://i.gyazo.com/4834feb5a33146e900d9b2e35d523301.png)](https://gyazo.com/4834feb5a33146e900d9b2e35d523301)

ターミナルを開いてください。クローンを保存したいディレクトリに移動します。ない場合は作成してください。

[![Image from Gyazo](https://i.gyazo.com/09b72e5cd9367ed3ab02badbc57fb897.png)](https://gyazo.com/09b72e5cd9367ed3ab02badbc57fb897)

`git clone`と入力した後にコピーしたコードを貼り付けます。
Enterキーを押します。

[![Image from Gyazo](https://i.gyazo.com/922de7caf4dbf6bd286f2c24f5fdd416.png)](https://gyazo.com/922de7caf4dbf6bd286f2c24f5fdd416)

これで自分のパソコンにクローンすることができました。



## 終わりに
- <h3>clone</h3>

**リモートリポジトリをローカルリポジトリにコピーすること**

同じ人間です。

- <h3>fork</h3>

**他人のリポジトリを自分のリポジトリにコピーすること**

DNAが同じだけど違う人間です。

---

クローン人間って別人だよな。。。とは思いますが。

これだけとりあえず覚えておきましょう。
深い話はまた別の機会に！！


<br>

> 参考サイト

- [GitHub Docs](https://docs.github.com/ja/github/getting-started-with-github/github-glossary#cron)
- [Qiita リポジトリのcloneとforkの違い](https://qiita.com/matsubox/items/09904e4c51e6bc267990)
- [Qiita 新人ではないがGit初心者であるエンジニアが「このリポジトリをフォークしてローカルで開発できるようにしておいて！」と言われた時にやること](https://qiita.com/sky0621/items/8b6e88f4327b42ade5d7)
- [GitHub のフォーク （fork） とプルリクエスト （pull request） の使い方](http://cuaoar.jp/2013/03/github-fork-pull-request.html#:~:text=%E3%82%AA%E3%83%AA%E3%82%B8%E3%83%8A%E3%83%AB%E3%81%8B%E3%82%89%E3%82%AF%E3%83%AD%E3%83%BC%E3%83%B3%E3%82%92%E4%BD%9C%E6%88%90,%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88%E4%BD%9C%E6%A5%AD%E3%82%92%E8%A1%8C%E3%81%84%E3%81%BE%E3%81%99%E3%80%82&text=GitHub%20%E4%B8%8A%E3%81%A7%E3%83%95%E3%82%A9%E3%83%BC%E3%82%AF%E3%81%97%E3%81%9F,%E3%81%97%E3%81%9F%E3%81%8B%E5%88%A4%E6%96%AD%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82)
