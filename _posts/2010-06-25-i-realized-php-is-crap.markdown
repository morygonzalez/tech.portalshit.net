---
id: 21
title: Rubyがエレガントだって言われるのがわかってきたような気がする
category: Ruby
layout: post
---

「PHPは汚い、Rubyはきれい」とかそういう言説の意味が昔は分からなかったんだけど、昨日今日、久々にCakePHPで作ったサイトのメンテナンスをしてて「PHP、確かにきちゃないわ」と思った。

オブジェクト指向っぽい何がしかのコードをPHPで書いてみる。

{% highlight php %}
<?php
class Hoge {
  var $a; 
  function hoge() {
    return $this->a = "hogehoge";
  }
}

$fuga = new Hoge();
echo $fuga->hoge();
?>
{% endhighlight %}

つぎにRubyで同じコードを書いてみる。

{% highlight ruby %}
class Hoge
  @a  
  def hoge
    @a = "hogehoge"
  end
end

fuga = Hoge.new
puts fuga.hoge
{% endhighlight %}

まずPHPは中括弧たくさん書かないといけない。これが面倒くさい。中括弧はキーボードでは `shift + [` とか `shift + ]` とかだから、 `shift` の分だけキーボードをたたく回数が増える。実にめんどい。最初はRubyのインデントでブロックを表現するところに慣れなかったけど、慣れたらちまちま中括弧をかかないとダメなPHPにいらいらするようになった。中括弧の閉じ忘れでエラーが出ることとかも多いし。

さらにメソッドとか変数へのアクセスもめんどい。Rubyだと `.` でアクセスできるのに、PHPだと `->` だ。入力するときはキーボードに `-` と `shift + .` と打たなきゃいけない。アホか。Rubyだとキーを一個打つので済むのが、PHPだと三個だ。

他にも予約語が長いとか、変数のスコープがおかしいんじゃねとか、Rubyを触る前は分からなかったPHPの変態的なところが目につくようになってきた。

PHPちゃん、僕もう疲れたよ（特にCakePHPの配列地獄）。
