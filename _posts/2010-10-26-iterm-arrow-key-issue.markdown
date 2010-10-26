---
id: 42
title: iTermでVimを使うと矢印キーでカーソル移動できない
categories:
- Vim
- Mac
layout: post
---

iTerm 2が素晴らしいということなのでiTermをぼちぼち使ってるんですけど、Vimを起動したときに矢印キーで移動できないことが分かった。「Vimで矢印キーでカーソル移動とか小学生かよ」みたいなご意見もあるでしょうけど、入力モードのときに移動したくなったら `j, k, h, l` じゃ移動できないでしょ？ そこで矢印キーですよ。

iTermでVimを使っているときも矢印キーでカーソル移動できないものかと、軽くググってみたところ次のような記事に遭遇した。

[MacBookのiTermでVimを使う時矢印キーで移動が出来ないときの解決方法 - Nobody is perfect.](http://d.hatena.ne.jp/takimo/20080308/1205047505 "MacBookのiTermでVimを使う時矢印キーで移動が出来ないときの解決方法 - Nobody is perfect.")

これを参考にとりあえず以下のように `.zshrc` に書いた。

{% highlight bash %}
case "${TERM_PROGRAM}" in
iTerm*)
  export TERM=dtterm
esac
{% endhighlight %}

しかし、これはちょっと自分的にはいただけなかった。

{% highlight bash %}
export TERM=dtterm
{% endhighlight %}

ってやると、termcap的な何かの作用で、Vimを閉じたときにコンソールを復元できなくなる（参照： [Vimで編集を終了した後、元のコンソールの状態を復元したい](http://tech.portalshit.net/2010/07/07/finish-editing-then-restore-console/ "Vimで編集を終了した後、元のコンソールの状態を復元したい | tech.portalshit.net - CakePHP, Rails, JavaScript")）。僕はVimを閉じた後はコンソールを復元したい派なので、このやり方は受け入れられなかった。

`.termcap` に何か書くことも考えたけど、 `.termcap` で条件分岐する書き方が分からなかったのでさらにググってみた。すると外人が「iTermの設定で何とかできる」みたいなことを書いてるのを発見した。

[Help2Go - free computer help and advice - Using Arrow Keys in iTerm with vi](http://www.help2go.com/Tutorials/Mac_OS/Using_Arrow_Keys_in_iTerm_with_vi.html "Help2Go - free computer help and advice - Using Arrow Keys in iTerm with vi")

なるほど、 `.vimrc` とか `.zshrc` とか側で回避する方法ばかり考えていたけどiTermで回避する方法を考えればよいわけか。

で、iTermを開いてみたところ、iTerm 1の頃から引き継いでいるBookmarkのDefaultの設定がよくなかったみたい。具体的には矢印キーそれぞれに `^[[A` とか `^[[B` みたいなキーが割り振られていて、このせいで矢印キーが使えなくなっていたわけだ。

Load Presetから "Use xterm Defaults" を選んでみたところ、無事矢印キーでカーソル移動できるようになった。めでたしめでたし。
