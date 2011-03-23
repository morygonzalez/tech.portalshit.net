---
id: 49
title: Ubuntuでは使うあてなくてもユーザーアカウントは複数作った方がいい
categories:
- Ubuntu
- zsh
layout: post
---

この前、さくらVPSに入れているUbuntuのzshで `ls` とか `cd` とか打ったとき、変なエラーメッセージが出るようになった。原因不明。しょうがないのでzshをインストールしなおそうと、`chsh` してbashとかに切り替えずに `sudo apt-get remove zsh` してしまった。そこで混乱してしまって `Ctrl + D` しちゃったもんだからSSH閉じてしまって、なんとUbuntuにログインできなくなってしまった。

Ubuntuは `root` というアカウントがなくてなんでも `sudo` するか、 `sudo su` で無理矢理rootになるしかないので、rootでログインしてchshしてやるという救済手段がとれず、にっちもさっちもいかなくなってUbuntuを再インストールした。

ちょっと調べたら、こういうアクシデントを防ぐために、/etc/shells にzshを足さず、chshでデフォルトシェルにもしないという人もいるみたい。`.bashrc` に次のように書くそうだ。

{% highlight sh %}
if [ -f /bin/zsh ]; then
  exec /bin/zsh
fi
{% endhighlight %}

これだと何かのトラブルでzshが起動しないことがあってもbashでログインできるということらしい。zshがちゃんとしてるときはzshでログインするという理屈だ。

[ウノウラボ by Zynga Japan: zshはじめました。](http://labs.unoh.net/2010/05/zsh.html)

しかしこれには結構重い副作用があるみたい。

[.bash_profileに「exec /bin/zsh」と書くのはやめたほうがいい - Humanity](http://d.hatena.ne.jp/tyru/20100922/exec_bin_zsh_considered_harmful)

一理ある。

というわけでUbuntuやrootでsshできない環境ででzshを使う場合は、何らかのトラブルでzshが起動しない、シェルにログインできなくなることを想定し、保険として普段はまったく使わない非常用のアカウントを作っておくと良いと思った。もちろんsudoersに指定しておかないと意味ないけどね。
