---
id: 29
title: oauth-pluginではまった
categories:
- Rails
- OAuth
layout: post
---

OAuthを導入しようとした。Twitterのだけなら何とか拾ってきたコードで動くとこまで持ってけてたけど、どうせやるならいろんなOAuth Providerに対応したい。oauth-pluginってgemを使えば簡単に沢山のOAuth Providerに対応できるみたいなので導入しようとしたけど、これがくせ者だった。

まずoauthとoauth-pluginをただ入れるだけじゃ動かない。 <q>acts_as_authenticated, restful_authentication  or restful_openid_authentication</q> というプラグインが入ってて、ユーザー認証をこれらのgemに任せてないとダメ。

作者がrestful_authenticationをすすめてたのでこれを導入した。（usersテーブルの構造自体が変わるので、ただ単にインストールするだけじゃなくて `rake db:drop` して古い `db/migrate/(日付)_create_users.rb` を削除し、もう一回 `rake db:migrate` しないといけない。さらにControllerとかViewとかもいじらなきゃいけないので地味に結構面倒くさい。

しかし何度やってもうまくいかない。「 `login_required` みたいなメソッドねーし」とかエラーが出る。どうやら昔の restful_authentication にはそういうメソッドがあったらしんだけど、現在の restful_authentication からは削除されてるらしい。他にも `current_user` っていうのも未定義で、この辺のエラーのおかげで完全に萎えた。

そういうわけで一週間くらいOAuth対応に向けて頑張ってたけど諦めました。TwitterだけOAuth認証に挑戦してみる。とってきたOAuth Tokenの扱いとかに若干不安があるけどうまくいくかしら。