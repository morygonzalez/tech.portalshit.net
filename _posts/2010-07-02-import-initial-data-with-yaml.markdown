---
id: 24
title: YAMLで初期データをRailsアプリケーションのDBにぶっ込む
categories:
- Rails
- YAML
layout: post
---

初期データをマイグレーションでRailsアプリケーションにぶっ込んでみた。後からいちいち手入力するのめんどいし、マイグレーションでデータをロードしとけば、本番環境でうごかすときも `rake db:migrate` で初期データは入るはずだから楽ちんかなと思って。

結果的には無事データをロード出来たんだけど、YAMLの書式が分かってなくて、結局丸一日時間を費やしてしまった。大したデータ量じゃなかったから下手するとちまちま手入力するのと変わらないくらい時間かかったかも。

{% highlight yaml %}
hoge: #アイテムの名前
  id: 1
  name: "hoge"
  address: "ホゲ県ホゲ村ホゲホゲ"

fuga:
  id: 2
  name: "fuga"
  address: "ホゲ県ホゲ村フガフガ"
{% endhighlight %}

とかやんなきゃいけなかったんだけど、YAMLの書き方が分かってなくて、

{% highlight yaml %}
hoge:
  id: 1
  name: "hoge"
  address: "ホゲ県ホゲ村ホゲホゲ"

  id: 2
  name: "fuga"
  address: "ホゲ県ホゲ村フガフガ"
{% endhighlight %}

とか書いてた。どっちも hoge県 に分類されるんでこんなんでいいだろ、みたいなノリ。しかしこれはやっぱり文書の構造がおかしい。これをロードしてみると、 id=2 のものしかロードされなかった。

結局、拾ってきた	コードを参考にして

{% highlight ruby %}
require 'yaml'
require 'pp'

data = YAML.load_file('hoge.yml')
pp data
{% endhighlight %}
		
みたいなやつを書いて、読み込まれる配列の構造を確認しながらYAMLを書いたところうまくいった。