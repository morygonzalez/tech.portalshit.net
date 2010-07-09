---
id: 27
title: OAuthがwakaranai
categories:
- Rails
- Ruby
- OAuth
layout: post
---

RailsでOAuthを使ってTwitterとかで認証させたい。oauth-pluginを使おうとしてるけど全然うまくいかない。イメージとしてはこんな感じ。

![OAuthの利用イメージ](images/27-oauth.png)

疑問点がいくつかある。

* Userモデルで `validate_presence_of` をパスワードフィールドにかけてるけど、OAuth経由でユーザーが追加されたときはどうすればいいんだろう。OAuth経由ではパスワードは預からないので、 `validate_presence_of` でエラーが出るはず。

* Userモデルで `has_many :oauth_tokens` とかリレーションの設定をしてしまったとして、OAuth経由ではなく普通にサインアップしたユーザーの扱いはどうなるんだろう？ 「 `oauth_tokens` にそんな `user_id` の人いないし」みたいなエラーが出るような気がする。

他にもいろいろ気になる点があったような気がするけど分からなくなってしまった。