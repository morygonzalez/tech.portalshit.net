---
id: 22
title: インスタンス変数
category: Ruby
layout: post
---

一個前の記事（[Rubyがエレガントだって言われるのがわかってきたような気がする \| tech.portalshit.net - CakePHP, Rails, JavaScript](http://tech.portalshit.net/2010/06/25/i-realized-php-is-crap/ "Rubyがエレガントだって言われるのがわかってきたような気がする \| tech.portalshit.net - CakePHP, Rails, JavaScript")）をcxxさんに添削してもらったところ、Rubyの方のコードには問題があったらしい。Rubyでは変数を宣言だけして終わりみたいな初期化をしちゃダメだそうで、必ず何かを代入しないといけないらしい。

そういうわけで正しくは、

{% highlight ruby %}
class Hoge
  def initialize
    @a = ""
  end

  def hoge
    @a = "hogehoge"
  end
end

fuga = Hoge.new
puts fuga.hoge
{% endhighlight %}

と書くそうです。

ところでなんで自分は前回、 `@a` というインスタンス変数を使ったのかがよく分からない。Railsでコードを書いていて、Controllerで定義した変数をViewで使うときにインスタンス変数を使うので、そういう風に思い込んでいるのかな。上のコードでは別にインスタンス変数を使う必要はなくて、

{% highlight ruby %}
class Hoge
  def initialize
    a = ""
  end

  def hoge
    a = "hogehoge"
  end
end

fuga = Hoge.new
puts fuga.hoge
{% endhighlight %}

でも同じ結果を出力しますね。

インスタンス変数と普通の変数の違いが分かってなかったので、たのしいRuby（第2版）を開いて復習してみたところ、以下のような記述があった。（たのしいRuby 第2版 pp.123-124）

> `@` で始まる変数は *インスタンス変数* といいます。ローカル変数とは違って、このメソッドを抜けてもその値は保存されますが、インスタンスごとに違う値を割り当てられる変数です。（たのしいRuby 第2版 pp.123-124）

なるほど！ 例えば上のコードを引数つきのものに改造したとしましょう。

{% highlight ruby %}
class Hoge
  def initialize(b="")
    @a = b
  end

  def hoge
    print @a, "\n"
  end
end

fuga = Hoge.new("Fuga")
piyo = Hoge.new("Piyo")

fuga.hoge
piyo.hoge
{% endhighlight %}

で、これを実行すると

{% highlight console %}
Fuga
Piyo
{% endhighlight %}

と表示される。こんな感じで、一つのクラスから複数のインスタンスを生成するときに使うのがインスタンス変数って理解でオーケーなのかなと思います。
