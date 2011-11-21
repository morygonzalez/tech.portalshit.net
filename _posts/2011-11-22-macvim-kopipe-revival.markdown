---
id: 63
title: MacVimでコピペできない問題の解決方法
categories: 
- tmux
- vim
layout: post
---


2011年はてなインターンであらせられるuasiさんのはてなブログに解決方法が書いてありました。

[Tmux で pbcopy/pbpaste が効かないやつ - uasi:ウアシー](http://uasi.hatenablog.com/entry/2011/11/15/150657 "Tmux で pbcopy/pbpaste が効かないやつ - uasi:ウアシー")

MacVimが悪いんじゃなくてtmuxに原因があったみたい。tmuxごしにVimを起動すると、MacVimでなくて普通のVimでもコピペができなくなる不具合があったようです。しかし[ChrisJohnsen/tmux-MacOSX-pasteboard - GitHub](https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard "ChrisJohnsen/tmux-MacOSX-pasteboard - GitHub")をインストールすることで解決します。tmuxだけでなくGNU Screen + Vimの組み合わせでも同様の問題が解決するそうです。お困りの方はお試し下さい。
