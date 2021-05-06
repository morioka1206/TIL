# bcyptとは
パスワードを暗号化してセキュリティを向上させるためのGemです。

## bcyptのインストール
Ruby on Railsの`Gemfile`の中にコメント付きで既に記述されていので
そのコメントアウトを外して`bundle install`することでインストールすることができます。

[![Image from Gyazo](https://i.gyazo.com/c196b9ec5a6fa16523c1d31c40dd8bda.png)](https://gyazo.com/c196b9ec5a6fa16523c1d31c40dd8bda)

[![Image from Gyazo](https://i.gyazo.com/1b8b2549ba959e3c50416f447702f709.png)](https://gyazo.com/1b8b2549ba959e3c50416f447702f709)

```terminal
% bundle install
```

## bycypt
bycyptでは主に2つのメソッドを使うことができるようになります。

- **has_secure_passwordメソッド**
- **authenticateメソッド**

#### ・has_secure_password
モデル内に１行書くことにより、**password**と**password_confirmation**という属性を使うことができます。

maigationファイルにカラムを追加する場合はpassword,password_confirmationではなく

```ruby:20210416072618_add_password_to_users.rb
class AddDetailsToTitles < ActiveRecord::Migration
  def change
    add_column :users, :password_digest, :string

  end
end
```
とする必要があるので注意です。

passwordを格納するデータベースのテーブルには**password_digest**というカラムを作成しておくと、
**password**と**password_confirmation**で入力したパスワードが一致していれば
**password_digestカラム**に暗号化してパスワードを格納することができるようになります。

viewファイルに`password`と`password_confirmation`をフォームで送るだけでbcyptが暗号化してくれます。

```erb:_form.erb

<%= form_with model: @user do |f| %>

  <%= f.label :password %>
  <%= f.password_field :password %>

  <%= f.label :password_confirmation %>
  <%= f.password_field :password_confirmation %>

<% end %>

```

#### ・authenticateメソッド
**authenticateメソッド**はパスワードを認証するためのメソッドで正しいパスワードを入力すると`true`を返し、間違ったパスワードを入力すると`false`を返します。

**パスワードのバリデーションは標準で装備されています。**

## アプリを作って試してみる
```console
% rails new password_app
```

```console
% cd password_app
```

```console
% rails db:create
```

```ruby:Gemfile
# gem 'bcrypt', '~> 3.1.7'
```
を外して

```console
% bundle install
```
Userモデルを作成してpassword_digestカラムを作成します。

```console
% rails g model user password_digest:string
```
作成できたら

```console
% rails db:migrate
```

userモデルにhas_secure_passwordを書きます。

```ruby:models/user.rb
class User < ApplicationRecord
  has_secure_password
end
```

rails consoleで動作確認します。

```console
$ rails c
```

[![Image from Gyazo](https://i.gyazo.com/8bc806567859bd4af89514802699d4eb.gif)](https://gyazo.com/8bc806567859bd4af89514802699d4eb)

間違ったパスワードを入れると`false`が返ってきて
正しいパスワードを入れると情報が返ってきています。

```console
irb(main):001:0> u = User.new
   (1.3ms)  SELECT sqlite_version(*)
=> #<User id: nil, password_digest: nil, created_at: nil, updated_at: nil>
```

```console
irb(main):002:0> u.password = "1234"
=> "1234"
```

```console
irb(main):003:0> u.save
   (0.2ms)  begin transaction
  User Create (3.6ms)  INSERT INTO "users" ("password_digest", "created_at", "updated_at") VALUES (?, ?, ?)  [["password_digest", "$2a$12$PaXO7LLKIqWGIXFhpkZcgOPSv2H.Mrmol6XwvI0aYMxrYdCFlmQCS"], ["created_at", "2021-05-06 13:04:13.549990"], ["updated_at", "2021-05-06 13:04:13.549990"]]
   (1.6ms)  commit transaction
=> true
```

```console
irb(main):004:0> u.authenticate("3333")
=> false
````

```console
irb(main):005:0> u.authenticate("1234")
=> #<User id: 4, password_digest: [FILTERED], created_at: "2021-05-06 13:04:13", updated_at: "2021-05-06 13:04:13">
```

以上です。

>参考サイト
[Qiita Railsにおけるパスワードの扱い方(BCrypt)](https://qiita.com/tatane616/items/c00182179e498aa9c53e)
[FREE SWORDER Railsアプリのパスワードを暗号化する方法〜bcryptの使い方〜](https://freesworder.net/rails-gem-bcrypt/)
[Rails Tutorial](https://railstutorial.jp/chapters/modeling_users?version=5.1#sec-adding_a_secure_password)
