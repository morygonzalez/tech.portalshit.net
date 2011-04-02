---
id: 17
title: Jekyllに変えた
category: misc
layout: post
---

このブログのCMSをMephistoから[jekyll](http://github.com/mojombo/jekyll "mojombo's jekyll at master - GitHub")に変えてみた。

Mephistoは公式サイトつながらないし、Mephisto使ってた外国のGeek連中がここ一年くらいでこぞってJekyllに移行してるみたいなのでこのビッグウェーブに乗ってみた。

### Jekyll = 静的CMS

しばらくJekyllの使い方が分からなくて格闘してたけど、やっと使い方が分かった。これは静的なCMSであって動的なCMSではない。Movable Typeに似てる。それをGeekなスタイルでやる感じ。

### Rubyが入ってるサーバーはいらない

コメント機能とかはないのでサーバーでRubyが動く必要はナッシング。DBも使わないのでMySQLの設定とかSQL分との格闘も必要ナッシング。コメント欄が欲しい場合は [DISQUS](http://disqus.com/overview/ "DISQUS \| Overview") とかに外注すればOK。

ちょっと話題がずれるけど、DISQUSって便利そうですよね。他人のブログにコメント書いたあとってそのコントロール権みたいのはブログの持ち主に移行するけど、DISQUSみたいなサービスを利用すればコメントを書いた本人が過去の自分のコメントをトラックしやすくなる。ブログ主にしたってスパム対策とかもやりやすくなる。自前で自分のブログにコメント欄を持つって時代は終わったのかもね。いまはTwitterとかもあるし。

### Mephistoからの移行について

Jekyllのgithubのwikiに移行方法が載っけてあるけど（[Blog Migrations - jekyll - GitHub](http://wiki.github.com/mojombo/jekyll/blog-migrations "Blog Migrations - jekyll - GitHub")）、これわかりにくい。というかMephistoをMySQLで運用してないとスクリプトをそのまんまでは利用できない。結果から書くと僕はMephistoはSQLite3で運用してたので移行スクリプトを使えなかった。

一応MephistoのDBをSQLite3からMySQLに変更してコンバートすることも試してみたけど、DreamHost上では `gem install mysqlplus` が `sudo` 権限がないために実行できず（なぜかユーザーディレクトリへのインストールもはねられる）、ローカルのMacBook上ではActiveRecordとかその辺でエラーが出て（MephistoはRails 2.2.2以下じゃないと動かないみたい）、Railsのバージョンを下げるとかも試してみたんだけどエラーが出続けるので諦めてしまった。

そういうわけでして、記事数が16本と少なかったこともあり、ちまちま手書きでMephistoからJekyllに移行しました。

コメント欄の設置（DISQUSを利用）とかフィードの生成とかカテゴリーの表示とかができてないけど、暇を見つけていじっていく予定です。

### 全般的なJekyllの使用感

DBいらずだしシンプルでいいっすわ。XML-RPCとかAPIを使ってどうのこうのとかいった機能はないけど、テキストファイルをしこしこ書いて、 .markdown か .textile みたいな拡張子で保存して、 `jekyll` コマンドを実行するだけでhtmlファイルが `_site` ディレクトリに生成されて、これをアップロードするだけ。この手順を自動化するシェルスクリプト（[tasks/deploy at master from henrik's henrik.nyh.se - GitHub](http://github.com/henrik/henrik.nyh.se/blob/master/tasks/deploy "tasks/deploy at master from henrik's henrik.nyh.se - GitHub")）も公開されているので、これを使えばectoとか使うのと変わらん感じでお手軽にブログ記事を投稿できます。

Terminalからコマンドライン打つの好きな人とか、軽くてシンプルなブログを求めてる人にはうってつけだと思いますね。
