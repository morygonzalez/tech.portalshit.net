---
id: 34
title: Pygmentsを使ってコードをシンタックスハイライトするようにした
category: Jekyll
layout: post
---


外タレのJekyllブログを見てると、シャレオツな感じでコードがシンタックスハイライトされてる。どうもPygmentsというやつを使うらしい。公式Wikiでも触れられていて、コードをハイライトさせたいときは `jekyll --pygments` しろや、みたいなことが書いてあるんだけど（[Liquid Extensions - jekyll - GitHub](http://wiki.github.com/mojombo/jekyll/liquid-extensions "Liquid Extensions - jekyll - GitHub")）、そういうオプションつけてもコードは全然色つきにならず、「サギやんけ」とか思ってた。

しかしマニュアルをよく読むと、PygmentsってのはPython製のソフトで、こいつを別途インストールする必要があるらしい。なるほどそういうことだったのか。そういうわけで

{% highlight console %}
  $ port search pygments
{% endhighlight %}

してみたところ、MacPortsでは三つヒットした。

{% highlight console %}
  py-pygments @1.0 (python, devel)
      Python syntax highlighter

  py25-pygments @1.0 (python, devel)
      Python syntax highlighter

  py26-pygments @1.3.1 (python, devel)
      Python syntax highlighter

  Found 3 ports.
{% endhighlight %}

しかしSnow LeopardにはPython 2.6.1が入ってるので、

{% highlight console %}
  $ easy_install Pygments
{% endhighlight %}

でもオッケーかも知れない。僕は職場に持ち込んでMacBookにはMacPortsから `py26-pygments` を入れた。そしたらdependencyが発動してPythonとかXorg何とかというもののダウンロードも始まり、 `/opt/local/bin/` に `python-2.6.5` が入ったが、長々と時間がかかった。<sup><a href="#footnote-34-1">※1</a></sup>

インストール完了後、これでシャレオツシンタックスハイライティングできるようになったと思い、意気揚々と

{% highlight console %}
  $ jekyll --pygments
{% endhighlight %}

してみたのだが、一向にハイライトされない。なんか「pygmentizeとか見つからないし」みたいなエラーが出る。なんでじゃ〜とイライラしながら公式Wikiを読んでると、次のような記述があった。

> the pygmentize binary must be in your path

そうなのよ。 `pygmentize-1.3.1` っていうバイナリファイルはあってパスは通ってるんだけど、 `pygmentize` そのものがないのよ。そういうわけで

{% highlight console %}
  $ sudo ln -s /opt/local/bin/pygmentize-1.3.1 /opt/local/bin/pygmentize
{% endhighlight %}

してやった。すると `pygmentize` というバイナリファイルにパスが通るので、めでたくシャレオツシンッタクスハイライティング環境が手に入った。ちなみにCSSは[Github互換のもの](http://github.com/mojombo/tpw/tree/master/css/syntax.css "syntax.css")を拾ってきて入れといた。

---

<p id="footnote-34-1">※1 この記事を書いている自宅のMacBook Proには `sudo easy_install Pygments` で入れてみたが、一瞬でインストール完了した。またシンボリックリンクを貼る手間とか必要なく、インストールしただけでパスも通ってた。そういうわけなのでMacPorts経由のインストールはオヌヌメしませんです。よい子のみなさんは `easy_install` しちゃいましょう。</p>
