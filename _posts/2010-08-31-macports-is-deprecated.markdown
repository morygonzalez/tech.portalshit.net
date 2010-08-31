---
id: 37
title: MacPortsからHomebrewに移行しつつある
category: Mac
layout: post
---

シャレオツプログラマーはみんなMacPortsからHomebrewに移行しつつあるっぽいので、真似してみることにした。

### なんでHomebrew？

そもそもなんでみんな移行するのか？ なんかMacPortsはバッドノウハウの塊らしい。

[Twitter / シャブ山シャブ彦: MacPortsはバッドノウハウの集合だったから，他 ...](http://twitter.com/hitode909/status/18526396749 "Twitter / シャブ山シャブ彦: MacPortsはバッドノウハウの集合だったから，他 ...")

MacPortsの何がバッドノウハウなのかちょっとよく分からなかったんだけど、でもよく考えてみたらMacPortsは `.bash_profile` とか `.zshrc` とかにへんてこりんなパスを埋め込まないといけないし、PerlとかRubyは一行目に `#!/usr/bin/perl` とか `#!/usr/bin/env ruby` とか書くのに使ってるバイナリ本体は `/opt/local/bin/` にあるとかは気持ち悪いっちゃ気持ち悪い。

HomebrewはLinuxのパッケージ管理ソフトみたいに `/usr/local/bin/` とかに何でもインストールするので精神衛生上ベターだ。

Homebrewのインストール自体は簡単だ。最近はそこそこRubyも分かるようになってきたので、パッケージ管理スクリプトをRubyで書くってのはなかなかよいかもしれない。詳しいことは公式Wikiとかを見て下さい。

[Homebrew — MacPorts driving you to drink? Try Homebrew!](http://mxcl.github.com/homebrew/ "Homebrew — MacPorts driving you to drink? Try Homebrew!")

### Vimのインストールではまった

Homebrew自体は簡単に入った。試しにVimをAppleがコンパイルしたVersion 7.2のものから新しめの7.3に上げて、ついでにRubyオプション入りでコンパイルしたかったので

{% highlight console %}
$ brew install vim
{% endhighlight %}

してみた。しかしながら

{% highlight console %}
Error: No available formula for dragonball
{% endhighlight %}

と出た。GUI版のMacVimはFormulaパッケージがあるらしいけど、フツーのVimはないらしい。「えー、自分でFormulaファイルを書かなきゃいけないの〜？」って感じだったんだけど、GitHubでテケトーに検索したらいろいろ出てきたので、 `/usr/local/Library/Formula/` に `vim.rb` を作ってコピペした。

[Library/Formula/vim.rb at duplicates from adamv's homebrew - GitHub](http://github.com/adamv/homebrew/blob/duplicates/Library/Formula/vim.rb "Library/Formula/vim.rb at duplicates from adamv's homebrew - GitHub")

そんで今度は意気揚々と

{% highlight console %}
$ brew install vim
{% endhighlight %}

してみたんだけど、なんとmakeに失敗する。Python.frameworkを参照してるときにエラーが出てるっぽい。

{% highlight console %}
ld: warning: in /Library/Frameworks//Python.framework/Python, missing required architecture x86\_64 in file
{% endhighlight %}

Appleが配布したのではないPythonを使ってるとこういうエラーが出るとかなんとか外人が言ってる。

[Nabble - Vim - Mac - Python link errors](http://vim.1045645.n5.nabble.com/Python-link-errors-td1214971.html "Nabble - Vim - Mac - Python link errors")

要するに64bit版のPython.frameworkを入れれば良さそうだった。何も考えずにHomebrewで `brew install Python` とかやって `/usr/local/bin/python` に新しいPythonを入れてみたりしたんだけど、これは意味なかったっぽい。大人しくPython公式サイトからPython 2.7のインストーラーパッケージをダウンロードしてきてGUIでインストールした。

[Releases](http://www.python.org/download/releases/ "Releases")

その後、もう一度 `brew install vim` をしてみたところ、無事make完了。`vim --version |grep ruby` で

{% highlight console %}
+ruby
{% endhighlight %}

となった。

まだApacheとかRubyGemsとかはMacPorts版を使っているけど、割と早い段階でHomebrewに移行して、シャレオツプログラマー仲間入りをしようと思います。
