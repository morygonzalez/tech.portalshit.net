---
id: 62
title: RVMをやめてrbenvにした
category: Ruby
layout: post
published: true
---

RVM、便利に使わせてもらっていたけど、Rubyの新しいのがリリースされるたびにいろいろアレだったので [rbenv](%link% "sstephenson/rbenv - GitHub") を使ってみることにした。移行、しんどいかなと思ってたけど非常に簡単で大変よかった。

### RVMのキモさ

RVMの悪いところはググればいろいろ出てくるけど、OSの `cd` やRubyの `gem` コマンドをシェルスクリプトで置き換えるとか、行儀が悪いところが問題らしい。個人的に気にくわなかったのがRVMがどんどんでかくなっていって、Rubyのビルドに必要なパッケージまで管理できるようになったところとか（.rvm以下に新しくシステムができるみたいな感じがキモかった）、パッケージインストール用のコマンドがhelpドキュメントでは `rvm package install` なのに `rvm pkg install` にいつの間にか変わっていて訳がわからないところとか、よくわからないシェルスクリプトがログイン時に実行されるところとか、 `rvmsudo` っていうコマンドのキモさとかいろいろ。

### rbenv

rbenvはRubyのバージョンを切り替えるためのツールなのでインストールはやってくれないけど、ruby-buildというツールを別に入れることで、 `rbenv install 1.9.2-p290` とかでRubyのインストールもこなしてくれるようになる。

あまりRVMを使いこなしてたとはいえなかった自分にとってはrbenvくらいでちょうどいいような感じがする。gemsetとか使わんし。そんくらいだったBundler使うし。

インストールは以下のページが参考になります。

[rbenv + ruby-buildのインストール方法 - 223 Software](%link% "rbenv + ruby-buildのインストール方法 - 223 Software")

なおrbenvはRubyインストール時のconfigureオプションの指定方法が特殊です。直接は指定できないようなので以下のようにします。（homebrewでインストールしたreadlineとiconvのパスを指定する例）

{% highlight console %}
$CONFIGURE_OPTS="--with-readline-dir=/usr/local --with-iconv-dir=/usr/local" rbenv install 1.9.2-p290
{% endhighlight %}

デフォルトのオプションなしのRubyだとearthquake.gemが動かなかったりjekyllが使えなかったりするので僕は↑のオプションを追加しました。よろしかったらお試し下さい。
