---
id: 45
title: RVMで入れたRubyをApacheとかから使いたい
category: Ruby
layout: post
---

RVMを使ってます。RVMで入れたRubyがshebangに `#!/usr/bin/env ruby` と書いたときに呼び出されて欲しいと思ってます。シェルから

{% highlight ruby %}
#!/usr/bin/env ruby

puts RUBY_DESCRIPTION
{% endhighlight %}

なファイル（hoge.rb）があったとします。これを

{% hilight console %}
$ ruby hoge.rb
{% endhilight %}

とシェルから呼び出したときにはちゃんと

{$ highlight %}
$ ruby 1.9.2p136 (2010-12-25 revision 30365) [x86_64-darwin10.6.0]
{% endhighlight %}

と表示されます。しかしTextMateでRunしたときや、Apacheから同じshebangで呼び出したときには、systemのRubyが呼ばれます。

これ、もう半年くらい解決方法探してる気がする。

TextMateでRunしたときにsystemのRubyが呼ばれるのはともかくとして（テストするときはシェルから呼び出すのでRVMのRubyで実行できる）、Apacheで新しめのRubyを使いたいときはどうすればよいのでしょう。まさかshebangに `~/.rvm/bin/ruby-1.9.2-p136` とか書くんじゃろか。

cxxさんに質問したら [RVM: Ruby Version Manager - Installing RVM System Wide](http://rvm.beginrescueend.com/deployment/system-wide/) というURLを教えてもらった。今日は眠いのでまた今度試す。
