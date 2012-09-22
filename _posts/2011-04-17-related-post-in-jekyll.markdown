---
id: 51
title: Jekyllで関連ポストを表示する
category: Jekyll
layout: post
---

### 関連記事表示

Jekyllで関連記事を表示するようにした。jekyllを実行するときに `jekyll --lsi` とするんだけど、Classifierというgemが必要。ただしClassifierを入れてるだけだと似てる記事を探すのにすんごい時間がかかるので、gslというgemを入れる。しかしこれはただ単に `gem install gsl` しただけでは以下のようなエラーが出る。

{% highlight console %}
Fetching: narray-0.5.9.9.gem (100%)
Building native extensions.  This could take a while...
Fetching: gsl-1.14.7.gem (100%)
Building native extensions.  This could take a while...
ERROR:  Error installing gsl:
        ERROR: Failed to build gem native extension.
        /Users/morygonzalez/.rvm/rubies/ruby-1.9.2-p136/bin/ruby extconf.rb
checking gsl version... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of
necessary libraries and/or headers.  Check the mkmf.log file for more
details.  You may need configuration options.

Provided configuration options:
        --with-opt-dir
        --without-opt-dir
        --with-opt-include
        --without-opt-include=${opt-dir}/include
        --with-opt-lib
        --without-opt-lib=${opt-dir}/lib
        --with-make-prog
        --without-make-prog
        --srcdir=.
        --curdir
        --ruby=/Users/morygonzalez/.rvm/rubies/ruby-1.9.2-p136/bin/ruby
extconf.rb:237:in `rescue in <main>': Check GSL>=0.9.4 is installed, and the command "gsl-config" is in search path. (RuntimeError)
        from extconf.rb:138:in `<main>'
{% endhighlight %}

GSL（GNU Scientific Library）が入ってないのがダメらしい。Homebrewでインストールする。

{% highlight console %}
$ brew install gsl
{% endhighlight %}

そんでもう一回 `gem install gsl` するとうまく入った。 `_config.yaml` に `lsi: true` という記述を追記して jekyll を実行すると関連記事が表示されるようになった。

### 最近の記事表示

ついでに見た目を調整した。サイドバーに全部の記事が表示されてたのがうざかったので10件だけ表示するようにした。

{% highlight diff %}
8c72..2c84ea5 100644
--- a/_layouts/post.html
+++ b/_layouts/post.html
7 +69,7 @@
 
         <h3>Latest Posts</h3>
         <ul>
-          {`% for post in site.posts `%}
+          {`% for post in site.posts limit:10 `%}
           <li><a href="{{ post.url }}">{{ post.title }}</a></li>
           {`% endfor `%}
         </ul>
{% endhighlight %}

(↑Liquidでエスケープする方法がわからんかったので {\`&#37; とかなってますけど、正しくは {&#37; です)

Liquidでは配列に対して <code>{&#37; for post in site.posts limit:10 &#37;}</code> という書き方をすることでループ処理の回数をコントロールできるみたい。

全体的に見やすくなりすっきりした。
