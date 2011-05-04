---
id: 54
title: MacVimでコピペできたんですけど…
category: vim
layout: post
---

MacVimでコピペできなくて（MacVim内のヤンクじゃなくて、他のアプリケーションでコピーしたもののペースト）困ってたんだけど（[MacVimでコピペできないんですけど… \| tech.portalshit.net](http://tech.portalshit.net/2011/04/23/macvim-kopipe-dekinai/ "MacVimでコピペできないんですけど… \| tech.portalshit.net")）、できるようになりました。原因は mvim っていう、コマンドラインからMacVimを起動するためのシェルスクリプトだった。MacVim kaoriyaのWikiで紹介されてるやつ。

* [src/MacVim/mvim at master from splhack/macvim - GitHub](https://github.com/splhack/macvim/blob/master/src/MacVim/mvim "src/MacVim/mvim at master from splhack/macvim - GitHub")

こいつ経由でMacVimを起動したときはどうも他のアプリケーションからのコピペがうまくいかないみたい。

同じくMacVim Kaoriya Wikiで紹介されている、MacVimを起動するコマンドをaliasで化したものを `.zshrc` に書いたところうまくコピペが機能した。

{% highlight bash %}
alias gvim='env LANG=ja_JP.UTF-8 open -a /Applications/MacVim.app "$@"'
{% endhighlight %}

同じ問題でお困りの方はお試しあれ。

### 追記

なんか違うっぽい。alias経由で呼び出してもダメなときはダメだもん。いったい何なんすかね。
