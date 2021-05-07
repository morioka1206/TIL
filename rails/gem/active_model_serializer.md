## はじめに

RailsでAPIモードでアプリケーションを作ったことすらないですが
active_model_serializersというGemについて学んだことをまとめておきます。

---

### シリアライズとは
>シリアライズとは、複数の並列データを直列化して送信することである。

>具体的には、メモリ上に存在する情報を、ファイルとして保存したり、ネットワークで送受信したりできるように変換することである。他方、既にファイルとして存在しているデータや、一旦シリアライズされたデータがネットワークから送られてきた際に、プログラムで扱えるようにする作業をデシリアライズと呼ぶ。

とのことですが、データをJSONで返すのもシリアライズされた結果のようです。
今回は置いておきます。。

----

　　
## active_model_serializersとはどんなGem?
active_model_serializersとはJSONを簡単にいい感じに整形してくれるGemらしいです。
他にも同じようなGemやjbuilder(APIの記事によく出てきました)のような機能はありますが

- **レスポンスが早い**
- **SerializerクラスにJSONを整形する処理をまとめられる**
- 直感的にわかりやすい書き方ができる

というメリットがあるようです。



## active_model_serializersの導入
`Gemfile`に記述してbundle installして導入します。

```ruby:Gemfile
gem ' active_model_serializers'
```

```console
% bundle install
```

## モデル生成
```console
% rails g serializer モデル名
```
このコマンドを実行することで、appディレクトリ下にserializersディレクトリが自動的に作成され、
指定したモデル名のファイルも作成されます。
例えば
```console
% rails g serializer user
```
とするとuser_serializer.rbが作成されます。
自動生成されたserializerファイルにいろいろな記述をすることで自由にJSONを整形することができます。

### JSONに含める値を追加、削除する
```ruby:app/serializers/user_serializer
class UserSerializer < ActiveModel::Serializer
  attributes :id
end
```
初期状態ではこのような形になっていますが
ここに表示したいモデルのカラム名を入れることでJSONに含めることができます。

```ruby:app/serializers/user_serializer
class UserSerializer < ActiveModel::Serializer
  attributes :id, :name, :email
end
```
nameとemailを追加しています。

controllerにシリアライザーを指定します
```ruby:users_controller.rb
class UsersController < ApplicationController
  def index
    users = User.all
    #このように指定します
    render json: users, each_serializer: UserSerializer
  end
end
```

```json:json
{
  "id": 1,
  "name": "Tom",
  "email": Tom@example.com
}
```

まだまだ理解が足りないので
随時追加していきます。



> 参考サイト
[Rails 6で認証認可入り掲示板APIを構築する #9 serializer導入](https://qiita.com/rf_p/items/be2c97c85253f4a1a914)
[gem Active Model Serializers のドキュメントを翻訳しました](https://qiita.com/ikamirin/items/be809c845f6104aa6f48#attributes%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88)
[Rails – ActiveModelSerializers gemでサクサクAPI開発](https://rooter.jp/programming/rails-activemodelserializers/#theme1)
[Railsのactive_model_serializerについて学ぶ_100DaysOfCodeチャレンジ10日目(Day_10:#100DaysOfCode)](https://qiita.com/yuta-ushijima/items/5bb947cedd96c01d75ca)
