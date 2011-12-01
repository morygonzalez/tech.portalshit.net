---
id: 64
title: RailsのViewでselectタグを使って生成されるoptionタグの中のvalueをエスケープする方法
category: rails
layout: post
---

Railsで画面を作っていて、DBを参照せずにselect -`>` option なHTML（ドロップダウンリスト）を出力したいと思った。DBに入ってない値をドロップダウンリストとして表示する方法。ググったらこういうやり方がヒットした。

[dropdownlist - Rails non-table drop down list - Stack Overflow](http://stackoverflow.com/questions/637787/rails-non-table-drop-down-list "dropdownlist - Rails non-table drop down list - Stack Overflow")

このやりが方がかっちょいいのかバッドノウハウなのか判別つかないけど、モデルに定数を書いてそこにいろいろ入れてしまうらしい。以下のような感じ。

{% highlight ruby %}
class Event < ActiveRecord::Base
  DAYS = ['Monday', 'Tuesday', 'Wednesday', ...]
end
{% endhighlight %}

でこれをモデルから参照するときは以下のようにする。

{% highlight ruby %}
<%= select(:event, :day, Event::DAYS) %>
{% endhighlight %}

これでうまいことドロップダウンリストを表示できる。

ところが一点問題があって、このドロップダウンリストで表示したい値が `"`（ダブルクオーテーション）を含んでいたとする。ダブルクオーテーションはRailsによって自動的にエスケープ処理されてしまうので、 `"` と表示させたいのに `&quot;` とか表示されてしまう。Form系のヘルパーメソッドで `text_area_tag` なら `:escape => false` とか出来るんだけど、`select` でそれをやるのは不可能だった。

Railsで文字列のエスケープをせずに出力する方法は一般的に

{% highlight ruby %}
<%= raw("文字列") %>
{% endhighlight %}

とか

{% highlight ruby %}
<%= "文字列".html_safe %>
{% endhighlight %}

だけど、「まさかそれをモデルの中でやっちゃってもエラー出るよね？」と思いながらやってみたらちゃんとエスケープせずにHTMLを出力できた。

モデルクラスのなかにヘルパーメソッドを書くのは気持ち悪いと思うけど、それ以外ではビューの中でイテレータを書いて一個一個エスケープしない処理を書くか、独自のヘルパーメソッドを書くしかない。なんかまどろっこしい気がするのでとりあえずこのやり方で行ってみることにします。
