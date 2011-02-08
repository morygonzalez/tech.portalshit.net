---
id: 46
title: RVMきもい
category: Ruby
layout: post
---

昨日の続きのようなもの。LokkaをUbuntu上で動かそうといろいろやってます。passenger入れて、 `passenger-install-nginx-module` を実行しようとしたらエラーが出た。お前はrootじゃないからnginxインストールできひんわ、みたいなメッセージが出る。sudoったりrootになってインストールしようとすると今度はpassengerなんていうgemはないわ、って怒られる。sudoしたときには.rvm内のgemパッケージではなくシステムのgemパッケージを見ようとするっぽい。またrootになるとRVMではなくシステムのRubyが実行されるので同じくpassengerなんてgemないわ、って怒られる。システムのRubyは1.8.7だし、なるべくなら使いたくない。RVMのRubyを使ってpassenger + nginxな環境作れないのかよ、とググってたら以下のような記事を発見した。

[Install RVM, Passenger, Nginx and Rails 3 on Ubuntu Lucid Lynx](http://www.blog.bridgeutopiaweb.com/post/install-rvm-passenger-nginx-and-rails-3-on-ubuntu-lucid-lynx/)

なんと、RVMには `rvmsudo` というコマンドがあるらしい！ 試しに

{% highlight console %}
$ rvmsudo passenger-install-nginx-module
{% endhighlight %}

を実行してみたところ、お前はroot権限がないんじゃ〜とエラーが出ていたところも無事通過してnginxをインストールできてしまった。以前、sudoで無理矢理nginxをインストールしたときは、 `nginx.conf` 内で、

{% highlight nginx %}
      passenger_root /home/morygonzalez/.rvm/gems/ruby-1.9.2-p136/gems/passenger-3.0.2;
      passenger_ruby /usr/bin/ruby1.8;
{% endhighlight %}

となっていて大変気持ち悪かったし、Passengerも「PassengerとRubyの本体でバージョンの不整合があるだろヴォケ」みたいな警告出してた。それが `rvmsudo` のおかげで `nginx.conf` に書き込まれる値も以下の通りとなるので、とりあえずPassenger（RubyGems）とRubyのバージョンが異なるというような問題は回避できる。

{% highlight nginx %}
      passenger_root /home/morygonzalez/.rvm/gems/ruby-1.9.2-p136/gems/passenger-3.0.2;
      passenger_ruby /home/morygonzalez/.rvm/wrappers/ruby-1.9.2-p136/ruby;
{% endhighlight %}

ただ、なんでか分からないのだけどnginxがうまく動いてくれなくて、無事Webサーバーを起動できてない感じです。

それにしてもRVMは、本当にきもいと思う。[readlineとかまで.rvm内にインストールできる](http://d.hatena.ne.jp/rochefort/20100907/p1 "rvmのirbで日本語入力できない - うんたらかんたら日記")できるし、いったい何考えてるんでしょうかね。きもすぎて便利です。