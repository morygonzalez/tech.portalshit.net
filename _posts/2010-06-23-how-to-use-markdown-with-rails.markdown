---
id: 20
title: RailsアプリケーションでMarkdownを使う
categories:
- Ruby
- Rails
layout: post
---

RailsアプリケーションでMarkdownを使いたと思った。（Markdown大好きっ子なので）

調べてみたところ、 [BlueCloth](http://deveiate.org/projects/BlueCloth "BlueCloth") というライブラリを使うといいらしい。

これはRailsのプラグインではないのでgemでインストール。

{% highlight console %}
$ sudo gem install bluecloth
{% endhighlight %}

その後viewで

{% highlight rhtml %}
<%= markdwon(@item.text) %>
{% endhighlight %}

とか書けばいい。

しかしなんも設定しない状態だとRailsアプリケーションはBlueClothを読み込まないので、config/environment.rbに

{% highlight ruby %}
config.gem "bluecloth"
{% endhighlight %}

と書いてやる。するとめでたくMarkdownが使えるようになる。
