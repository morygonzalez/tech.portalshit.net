---
layout: post
categories:
- Ruby
- Mac
title: Homebrew で入れた libなんとかとのうまいつきあい方が知りたい
date: 2012-03-09 10:59:03
published: false
---

Homebrew で rbenv と ruby-build をインストールし、Ruby をインストールしている。Nokogiri をインストールしようとするとlibiconv が足りないとエラーがでる。Nokogiri のインストールマニュアルを見ると以下のようなことが書いてある。

<blockquote>
<h3 id="homebrew_08_or_later">homebrew 0.8 or later</h3>
<pre><code>brew install libxml2 libxslt
brew link libxml2 libxslt
gem install nokogiri</code></pre>
</blockquote>

言われたとおりにシンボリックリンク張って、さらに libiconv にもシンボリックリンクはった。この状態だとちゃんと Nokogiri 入る。入るが、

{% highlight console %}
brew doctor
{% enbhighlight %}

