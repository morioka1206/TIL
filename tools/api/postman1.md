![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1111652/6d5cb49b-e8f7-2755-a8ac-84bc277bec16.png)

## はじめに
みなさん**Postman**は知ってますか？
郵便配達じゃなくて、WebAPIのツールです。
WebAPIを勉強しようと思ったときに、便利なツールがあるということでまずはPostmanを触れてみようと思います。

今回は**GETメソッド**を使って〠郵便番号を取得してみましょう。

## Postmanとは
[![Image from Gyazo](https://i.gyazo.com/64b296b0cddd544a08ef484c6be039b1.png)](https://gyazo.com/64b296b0cddd544a08ef484c6be039b1)
Postman(ポストマン)はPostman社が提供しているAPI開発用のコラボレーションプラットフォーム。APIを開発する作業を簡素化してくれて、作業効率を向上してくれます。

リクエストから認証、テストなどの機能が搭載されていてAPI開発をスピーディーに行えるようになります。

## Postmanの機能
Postmanの大まかな機能は6種類あります。
[![Image from Gyazo](https://i.gyazo.com/92868826790944b80dfa425287852feb.png)](https://gyazo.com/92868826790944b80dfa425287852feb)

- **API Client**
公開されているもしくは開発中のAPIをテストできる機能

- **Autimated Testing**
マニュアルテストを自動化してCI/CDパイプラインに統合する

- **Design & Mock**
バックエンドサーバーを設置せずにエンドポイントとレスポンスをシュミレート

- **Documantation**
自動的にAPIドキュメントを生成して公開できる機能

- **Monitors**
APIのアップデートや変更に伴う破損や変化がないかをモニタリングする

- **Workspaces**
チームでAPIを共同開発するための機能

## Postmanのインストール
PostmanはWebアプリケーションとしても使うことができますが、ダウンロードして使うこともできます。

[Postmanダウンロードページ](https://www.postman.com/downloads/)

[![Image from Gyazo](https://i.gyazo.com/5984050649349edc4bce63a354e2e3b3.png)](https://gyazo.com/5984050649349edc4bce63a354e2e3b3)

インストールするとサインアップを求めらるのでメールアドレスなどを入力してサインアップします。

[![Image from Gyazo](https://i.gyazo.com/27ca3a1540e744cf27b4a95efa8a0aab.png)](https://gyazo.com/27ca3a1540e744cf27b4a95efa8a0aab)

ログインするとホーム画面が表示されます。

[![Image from Gyazo](https://i.gyazo.com/bfb1c6a8205643ecfde9d9e056ad37bc.png)](https://gyazo.com/bfb1c6a8205643ecfde9d9e056ad37bc)

**Create New**をクリックしてください。

[![Image from Gyazo](https://i.gyazo.com/3543734b3628f6ec8a008208f892a345.png)](https://gyazo.com/3543734b3628f6ec8a008208f892a345)

それでは郵便番号から住所を取得していきましょう。

今回はzipcloudという郵便番号配信サービスを使ってJSONを取得してみます。
[zipcloud](http://zipcloud.ibsnet.co.jp/doc/api)

[![Image from Gyazo](https://i.gyazo.com/bdb18b4da8f59b540e53635a1c854ed7.png)](https://gyazo.com/bdb18b4da8f59b540e53635a1c854ed7)

[![Image from Gyazo](https://i.gyazo.com/bfe105b4d4bae2eade57d7e6a6d58cc3.png)](https://gyazo.com/bfe105b4d4bae2eade57d7e6a6d58cc3)

リクエストURLの`https://zipcloud.ibsnet.co.jp/api/search`を貼り付けます。

[![Image from Gyazo](https://i.gyazo.com/580550c16d908e051340eaf80f32d039.png)](https://gyazo.com/580550c16d908e051340eaf80f32d039)

ここに郵便番号を入力するだけでも検索することができます。

```console
https://zipcloud.ibsnet.co.jp/api/search?zipcode=郵便番号
```
とURLの後にパラメータ名と検索したい郵便番号を入力してみましょう。

[![Image from Gyazo](https://i.gyazo.com/18241934f8aee263f89d679d2d93cf72.png)](https://gyazo.com/18241934f8aee263f89d679d2d93cf72)

入力するとわかるかと思いますがKEYとVALUEが自動で入力されます。
逆にVALUEを変更するとURLの値も自動で変わります。

[![Image from Gyazo](https://i.gyazo.com/5bb8c9fac127b048751c10d278c3efb7.gif)](https://gyazo.com/5bb8c9fac127b048751c10d278c3efb7)


郵便番号で住所は取得できましたでしょうか？
こんな感じでPostmanは簡単にしかも、見やすくAPIを試すことができます。

便利な機能はたくさんありますが今回はここら辺で。

<br>
> 参考サイト
- [Zenn 圧倒的業務効率化！Postman の便利な使い方](https://zenn.dev/susiyaki/articles/525a58277233acdb3f73)
- [XLSOFT BLOG RESTサービスを触る際の必須ツールPostmanを使ってみました](https://www.xlsoft.com/jp/blog/blog/2017/06/23/post-1638/)
- [IT業務で使えるプログラミングテクニック Postmanを使ったAPIテストのやり方](https://kekaku.addisteria.com/wp/20180606063858)
