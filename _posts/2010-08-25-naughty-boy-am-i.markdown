---
id: 35
title: Naughty BoyなのでCakePHPのDBもRailsのActiveRecordを単体で使って操作してやった
categories:
- Ruby
- Rails
layout: post
---

80個近くある静的HTMLファイルをシステム化する必要が生じたので、HTMLをHpricotでスクレイピングしたあと、抽出したデータをSQLiteにぶっ込んだ。しかしSQLiteにぶっ込んだあとでデータの一部をいじりたくなった。そこでRailsのActiveRecordを単体で使ってみた。

### なんでわざわざActiveRecordを使うのか

いやそりゃもちろんSQL書くのが怖いからですよ。というのは半分冗談なんですけど、CakePHPはSQLite 2にしか対応しておらず、SQLite 2は何かと制限が多い。replace関数が使えんとか。temp tableとか作るのかったるいし、フレームワークばっかり使っててSQLはあんまりよく分からないのでActiveRecordを使った次第です。

### 作業詳細

このシステム化するプロジェクト自体はCakePHPで動いており、DBはSQLite2。デフォの状態だとRailsは `sqlite3-ruby` しかインストールしないので、ActiveRecordからSQLite2なDBを操作することができず若干まいっちんぐだったんだけどなんとかでけた。ちなみにやったのはCRUDのReadとUpdateね。

#### やったこと

とりあえず以下のようなファイルを用意。各レコードの `name` フィールドの "hogehoge" という部分なのが邪魔なので削りたかった。

{% highlight ruby %}
#!/usr/bin/env ruby

require "rubygems"
require "sqlite"
require "active_record"

ActiveRecord::Base.establish_connection(
  :adapter => "sqlite",
  :database => "path/to/db"
)

class Hoge < ActiveRecord::Base
end

hoges = Hoge.find(:all)
hoges.each do |hog|
  hog.name.gsub!(/hogehoge/, "")
  hoge.save
end
{% endhighlight %}

まず最初に、 `no such file to load -- sqlite` みたいなエラーが出た。要するに「お前SQLite 2のアダプター入れてねえだろ」というエラー。とりあえず `sudo gem install sqlite-ruby` したんだけど、それでも `no such file to load — sqlite` が出るのでMacを再起動したら「Rails 3ではSQLite 2はdeprecatedだからさっさとSQLite 3に移行しろや」みたいなメッセージは出るもののちゃんとDBの内容を読み込めた。CRUDのReadはでけた。

しかしUpdateの部分で失敗。Railsの感覚で `hoge.save` とかやったんだけどこれは意図したとおりに機能しなかった。しょうがないのでRailsのAPIリファレンスを見ながら、 `update_attribute()` というメソッドをぶちかましてやった。こんな感じ。

{% highlight ruby %}
hoges.each do |hog|
  if hog.name =~ /hogehoge(.*)/
    hog.update_attribute("name", $1)
  end
end
{% endhighlight %}

これで狙ったことができました。

Rubyいいわー。ほんといいわー。