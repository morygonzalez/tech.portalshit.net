---
id: 59
title: RVMでRubyをアップグレードしたら "bad interpreter" という警告が出る
categories:
- rvm
- Ruby
layout: post
---

Ruby 1.9.2-p290 がリリースされたので入れてみた。RVMで。

{% highlight console %}
rvm install 1.9.2 --with-readline-dir=/usr/local #homebrewで入れたreadlineのパスを指定
rvm migrate ruby-1.9.2-p180 ruby-1.9.2-p290
{% endhighlight %}

`migrate` を実行したところ、警告が出ながらも次のような感じでマイグレーションは完了した。

{% highlight console %}
rvm migrate ruby-1.9.2-p180 ruby-1.9.2-p290
Are you sure you wish to MOVE gems from ruby-1.9.2-p180 to ruby-1.9.2-p290?
This will overwrite existing gems in ruby-1.9.2-p290 and remove them from ruby-1.9.2-p180 (Y/n): Y
Moving gemsets...
Moving ruby-1.9.2-p180 to ruby-1.9.2-p290
Making gemset ruby-1.9.2-p290 pristine.
ERROR: Error running 'rvm gemset pristine' under ,
please read /usr/local/rvm/log//gemset.pristine.log
Moving ruby-1.9.2-p180@global to ruby-1.9.2-p290@global
Making gemset ruby-1.9.2-p290@global pristine.
ERROR: Error running 'rvm gemset pristine' under ,
please read /usr/local/rvm/log//gemset.pristine.log
Do you wish to move over aliases? (Y/n): Y
Do you wish to move over wrappers? (Y/n): Y
Do you also wish to completely remove ruby-1.9.2-p180 (inc. archive)? (Y/n): Y
Successfully migrated ruby-1.9.2-p180 to ruby-1.9.2-p290
{% endhighlight %}

一見、問題なく移行できたように思えるのだけど、この後rakeなどexecutableなgemをコマンドラインから実行すると以下のようなエラーが出る。

{% highlight console %}
zsh: /usr/local/rvm/gems/ruby-1.9.2-p290/bin/rake: bad interpreter: /usr/local/rvm/rubies/ruby-1.9.2-p180/bin/ruby: no such file or directory
rake aborted!
No Rakefile found (looking for: rakefile, Rakefile, rakefile.rb, Rakefile.rb)
/usr/local/rvm/gems/ruby-1.9.2-p290/gems/rake-0.8.7/lib/rake.rb:2377:in `raw_load_rakefile'
(See full trace by running task with --trace)
{% endhighlight %}

shebangに書いてあるrubyのパスがmigrate時に削除した ruby-1.9.2-p180 なのが問題なわけだ。

正しい対処方法かどうかは自信がないが、Rubyでサクサクッとshebangを書き換えるやつを書いた。以下みたいなやつ。

<script src="https://gist.github.com/1092544.js?file=fix_shebang.rb"></script>

こいつを実行してやるとshebangが正しく書き換わったexecutableなgemができる。万が一のためにbackupファイルを作るのでこれをzshで `rm *_backup` とかしてやるといいと思います。

と思ったけど、結局↑のRubyの入れ方はまずいみたいで、jekyllとかCライブラリに依存する系のgemが動かなくなってしまったので `rvm implode` してRVMをまるっと入れ替えた（20回くらいRubyをインストールしなおした）。次の記事にでも書きます…。
