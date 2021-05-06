# ruby-jwtとは

**サーバーサイドのログイン認証**に使う。
JWTを使いログイン認証機能を実装する。
ログイン時にJWTをCoookieに保存し、アクセスじにはそのJWTが有効であるかを検証する機能。
<br>
  
    
<br>
 
## JWT認証とは
**JWT**（ジョット）とはJSON WebToken(ジェイソンウェブトークン）の略で２つのパーティー間で
情報を安全に送信する方法。
JSONオブジェクトをエンコードした文字列で、この文字列を**トークン**と呼ぶ

```
eyJhbGciOiJIUzI1NiJ9.
eyJleHAiOjE2MDA1OTY0MzEsInN1YiI6MSwibmFtZSI6InVzZXIwIn0.
lXcwASyLX5GEsMvPYDVhe0ovJj631fUiC0q2ojK-yK0
```
<br>

## 3つのトークン
JWTが発行したトークンはドットによって3つに分かれており、それぞれの情報を保持している。

```
<ヘッダ>.<ペイロード>.<署名>
```

### 1.ヘッダ
最初の文字列をヘッダと呼びます。
ここにはトークンのタイプや、使用されている署名アルゴリズムの情報を持っています。

```
// エンコード => デコード
eyJhbGciOiJIUzI1NiJ9. 
=> { "alg": "HS256", "typ": "JWT" }
```

<br>

### 2.ペイロード
２番目の文字列をペイロードと呼び、任意の情報を指定することができます。
基本的には、このペイロードをカスタマイズしてユーザー認証に必要な情報を埋め込みます。

```
eyJleHAiOjE2MDA1OTY0MzEsInN1YiI6MSwibmFtZSI6InVzZXIwIn0. 
=> {"exp"=>1600596431, "sub"=>1, "name"=>"user0"}
```

またこの`exp`や`sub`などのそれぞれの値を**クレーム**と呼びます。

デフォルトで指定されているものを**予約クレーム**、使用者が任意に指定した値を**パブリッククレーム**と呼びます。
  
<br>

  
### 3.署名
３番目の文字列には署名情報が入っています。
この署名はトークンが変更されていないか確認するために使用されます。
```
// エンコード => デコード
lXcwASyLX5GEsMvPYDVhe0ovJj631fUiC0q2ojK-yK0
=> HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  your-256-bit-secret
)
```

## JWTのメリット
1. 情報が改竄できない
2. ユーザーテーブルにトークンを一時的に保有するカラムを作成しなくていい
3. 署名をした鍵を持つものしかトークンを検証することができない

## JWTの注意点
トークンはエンコードされているだけで、暗号化はされていない。
トークンはjwt.ioで誰でも見ることができる。[jwt.io](https://jwt.io/introduction/)
漏洩したらまずい個人情報はトークンに組み込まないようにする。

## Railsにruby-jwtをインストール
```ruby:Gemfile
gem 'jwt'
```
<br>

```
% bundle install
```

## JWTを発行する

### ペイロードの作成

Railsコンソールに入ってトークンを発行してみる
```
rails c
```

まずは任意の情報を埋め込むペイロードを作成します。

```
> payload = { sub: 1 }
```

#### sub(Subject)クレーム
JWTの守護となる主体の識別子で予約クレームの一つ。
一般的にはオブジェクトを識別する一位の値を指定する。
ユーザーテーブルで言うとユーザーIDのこと。

`{user_id: }`といったものでもいいが他アプリケーションとの衝突を避けるために予約クレームを使用することが推奨されています。

>[予約クレーム一覧](https://openid-foundation-japan.github.io/draft-ietf-oauth-json-web-token-11.ja.html#ReservedClaimName)

### 鍵の指定
トークン発行には署名時に使用する鍵が必要です。
この鍵が漏れると誰でも発行と検証ができるので、非公開鍵であるRailsのシークレットキーを使用します

```
> secret_key = Rails.application.credentials.secret_key_base
```

### JWTを発行する
トークンの発行には`JWT.encode`メソッドを使う。
```
> token = JWT.encode(payload, secret_key)
> token
> => "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOjF9.ZY3-9YTmrTz8H0t22DkyGREF_IZCgFkNoMjzHSGN_8U"
```

- `JWT.encode(payload, key, algorithm = 'HS256', header_fields = {})`
  - `algorithm`　署名アルゴリズム。デフォルトでは`HS256`が指定されている。
  - `header_fields`　ヘッダーフィールド。ヘッダー部分に埋め込む情報をハッシュで指定します。

### JWTをデコードする
発行したトークンの中身を確認するには、`JWT.decode`メソッドを使います。

```
> JWT.decode(token, secret_key)
=> [{"sub"=>1}, {"alg"=>"HS256"}]
```
- `JWT.decode(jwt, key, verify = true, options = {})
  - `verify`　バリデーションの有無。必ず`true`を指定する。ここで`false`を指定した場合はトークンが改竄されてもエラーが出ない。
  - `options`　追加オプションの指定。デフォルトのオプションは[ここ](https://www.rubydoc.info/github/jwt/ruby-jwt/JWT/DefaultOptions#DEFAULT_OPTIONS-constant)から確認できます。

署名時に付けた鍵と同じ鍵を使って検証する署名アルゴリズム**「HS256」**、
秘密鍵と公開鍵のペアで検証する署名アルゴリズム**「RS256」**

