## はじめに
Vue.jsをRailsで使うときにバックエンドをRailsのAPIモードで作り、
フロントエンドをVue.jsで作る記事をよく見かけた。
その際にルーティングでnamespaceを使っていたけれど
なぜnamespaceを使うのかよくわからず、苦手意識があったので理解するためまとめてみました。

まずはAPIとはそもそもなんぞやというところからはじめてみましょう。

## APIとは
APIはApplication Programming Interfaceの略です。
ソフトウェアの機能を共有できる仕組みのこと。よく使われているものだとGoogle Mapなど。
郵便番号を入れると自動で入力されるなんてことができるのもこれのおかげだったり。

APIは通常Webに公開されていて、誰でも無料で使うことが可能。「WebAPI」と呼ばれたりもします。
一般的にJSONという形式で結果を返します。

### RailsのAPIモードとは
RailsのAPIモードはそのAPIをRailsで作成できるAPI作成に特化したモードのこと。
APIモードではMVCのViewg作成されません。
そのため、sass-railsやwebpacker、capybabaraなどはGemfaileには生成されません。

Rails4までは`rails-api`というgemを入れる必要があったみたいですが
現在のバージョンでは特に何もしなくても使えます。

```console
rails new アプリケーション名 --api
```
と打つだけでAPIモードのRailsアプリケーションが作成されます。

次にそもそもnamespaceってなにという疑問を解消していきます。


## Railsのルーティング
RailsのルーティングはMVCモデルの基本の基本と言えるもので
Viewから送られたリクエストを適切なコントローラーに送り、どんなアクションを行うかを管理するものです。

ルーティングはRailsアプリケーションのconfigディレクトリの中にある`routes.rb`に記述します。

##### Railsルーティング種類は調べてみるとたくさんありました。
- **urlを直接指定する**
- **root**
- **resouce**
- **resouces**
- **collection**
- **member**
- new
- **param**
- **shallow**
- **namespace**
- **scope**
- **concern**
- **constraints**

などなどたくさんあります。深そうですね。。。


## scopeとnamespaceの違い
ルーティングのまとめは別の機会にするとして
今回はその中で**namespace**にフォーカスを当てていきますが、
namespaceと似たようなscopeとの比較してみます。


|             |scope                  |namespace      |
|-------------|-----------------------|---------------|
|URL          |指定のパス　　　　　　　　　|指定のパス       |
|コントローラ　　|通常のcontroller内　　　 |controllerの中の指定のフォルダ|


scopeもnamespaceもURLを指定のパスにできますが
namespaceはファイル構成も変えたい場合にいいみたいです。
scopeでもいいような気もしますね。


##APIのバージョン
railsのAPIを調べているとnamespaceを使ったroutes.rbの

```ruby
Rails.application.routes.draw do
  namespace 'api' do
    namespace 'v1' do
      resources :posts
    end
  end
end
```

などのところにある**v1**という記述。
調べてみるとバージョン１の意味でした。
バージョン管理をするために**scope**ではなく、**namespace**を使っているのかとAPIのバージョン管理とは
なんぞやと調べていきます。

## Web APIのバージョン管理の重要性
Web APIとはアプリケーションのインターフェイスの役割を持ち、追加、変更、廃止などされていくものです。
通常のアプリもver.1.0.8とか書かれていますよね。
[セマンティックバージョニング](https://semver.org/lang/ja/)と言います。

バージョン管理を特にせず、管理者がこっちの方がいいから変更しよう〜とAPIを書き換えてしまったら
そのAPIを使っているユーザーがいきなり使えなくなってしまう可能性があります。

例えばFacebookやGoogleなどのAPIが急に変更されると
エラーが出て処理が止まったり、表示がおかしくなるなどの不具合が発生します。

それを防ぐために公開されているAPIは複数のバージョンを提供して、
そういう事態を招くことを防いでいるわけです。

#### APIのURI一覧

- DMMのAPI
https://api.dmm.com/affiliate/v3/ItemList?api_id=[APIID]&affiliate_id=[アフィリエトID]&site=DMM.R18&service=digital&floor=videoa&hits=[検索数]&sort=date&keyword=[キーワード]&output=[jsonかxml]

- TwitterのAPI
https://api.twitter.com/2/tweets/search?tweet.fields=created_at,author_id,lang&query=$QUERY"

- YouTubeのAPI
https://developers.google.com/youtube/v3/docs/

- FacebookのAPI
https://graph.facebook.com/v2.0/me

とURIの中を見てみると、v○とあります。

いくつかバージョンの管理方法があるようなのですが
**URIにバージョンを埋め込むのがよく利用される方法**のようです。

## まとめ
これらから考えられることはWeb APIは一人のユーザーが利用するものでなく、
アプリケーションと同様に多くの人が利用するために作られるためバージョン管理がされている。
その慣例としてv1などのバージョンをつけてルーティングをつけている。
それを実現するにはscopeよりもnamespaceが良いため、namespaceでルーティングをしていることが考えられる。



## 終わりに
RailsでAPIを作るとなったときに
知らないnamespaceなどが出てきてよくわからなくて混乱しましたが
なぜそうしているのかを時間はかかりますが紐解くのは大事です。

さまざまな記事を読ませていただいたのですが、それ違うなどもあると思いますので
ぜひご指摘いただけたら嬉しいです。


>参考サイト
[Railsのルーティングの種類と要点まとめ
](https://qiita.com/senou/items/f1491e53450cb347606b)
[初心者じゃなくても役に立つかもしれないRailsのroutingの記述方をまとめてみた](https://shiro-16.hatenablog.com/entry/2015/03/19/001656)
[routeのmoduleとnamespaceとscopeの違い
](https://qiita.com/blueplanet/items/522cc8364f6cf189ecad)
[Railsのroutingにおけるscope / namespace / module の違い
](https://qiita.com/ryosuketter/items/9240d8c2561b5989f049)
[きゃまなかのブログ 【Ruby on Rails】ルーティング scope と namespace の違い](https://techblog.kyamanak.com/entry/2017/07/30/223113)
[RESTfulにするためRailsのルーティングをresources,namespace,scopeだけで頑張る](https://cre8cre8.com/rails/resources-namespace-scope-routes.rb.htm)
[Rubyの名前空間（namespace）について現役エンジニアが解説【初心者向け】](https://techacademy.jp/magazine/22391)
[REST API利用時のNamespaceの重要性(RESTとGraphQLの比較とかも）](https://qiita.com/matsukazu1112/items/ab46a2d226c70be7649d)
[Web API: The Good Partsを読んだまとめ](https://qiita.com/mitsuya/items/e33d5ac202b41447cfec)
[Web API: The Good Partsを読んだので「設計変更しやすいWeb API」についてまとめた](https://qiita.com/soyanchu/items/34f8e164c24f044e80a3)











