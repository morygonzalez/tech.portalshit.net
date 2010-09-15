---
id: 39
title: RVMのRubyをTextMateで使う
category: Ruby
layout: post
---

いやまぁテキストエディターにはいろいろあるわけでして、皆さんEmacsとかVimで日夜しこしこコードを書いておられると思うんですけど、僕はGUIしか使えない情報弱者なので主にTextMateを使ってます。

TextMateで便利なのが "Run" っていう機能です。Rubyのコードを書いていて、<kbd>&#8984;</kbd> + <kbd>R</kbd> でさくっと実行結果を確認できます。いちいちTerminal開いて

{% highlight console %}
$ ruby hogehoge.rb
{% endhighlight %}

とか面倒くさいことうやらずにすみます。

で、これからが本題なんですけど、先月Ruby 1.9.2がリリースされて、さらに `gem update` でRails 3が入るようになってしまったので、お試しでRuby 1.9.2とRails 3を使ってみることにしました。しかし1.8系を完全に捨てることは恐ろしいので、RVMを使って複数のバージョンのRubyを切り替えながらしばらく過ごしてみることにしたわけです。

上に書いたとおり僕ちゃんは情報弱者なのでTextMateに依存したコーディングライフを送っており、<kbd>&#8984;</kbd> + <kbd>R</kbd> で動くRubyもRVMのRubyにしたいと思ったのですが、これが分からなかった。RVMのサイトを見たらいろいろごちゃごちゃやり方が書いてあるんだけど（[RVM: Ruby Version Manager - Textmate Integration with RVM](http://rvm.beginrescueend.com/integration/textmate/ "RVM: Ruby Version Manager - Textmate Integration with RVM")）、結局この通りにやってもうまくいかず。

しかし先ほどなにげなく

{% highlight console %}
$ rvm 1.9.2 --default
{% endhighlight %}

としてあげたところ、TextMateでもRVMのRubyが走るようになりました。