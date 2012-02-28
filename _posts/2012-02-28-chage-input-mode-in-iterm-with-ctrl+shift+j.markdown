---
layout: post
category: Mac
title: iTerm で Ctrl + Shift + J でかな入力変換する方法
date: 2012-02-28  9:41:46
---

Mac の iTerm 2 皆さん使ってますか。コンソール中に現れた文字列をハイライト通知できたりしていろいろ便利らしいですね。でも僕は使っていませんでした。なぜか。

*`Ctrl + Shift + J` によるかな入力変換ができないから。*

これが非常にだるかった。宗教上の理由や国外在住でJISキーボードが手に入らないなどの理由のためやむなく英語キーボードを使っている方、おられると思います。そういう人はだいたい `Ctrl + Shift + J` で英数 -> かなの入力変換を行っていると思いますが（`Command + Space` の切り換えもできなくはないけどだるいですよね…）、iTerm 上では `Ctrl + Shift + J` で改行が行われてしまうため、このような操作が行えていませんでした。かなから英数入力に切り替える `Ctrl + Shift + *` も同様、むなしく `'` などが表示されるだけ。標準の Terminal.app ではできるのになんでやねん。

[iTermでの日本語入力 - 初学者の箸置](http://d.hatena.ne.jp/tkuro/20091124/1259039460 "iTermでの日本語入力 - 初学者の箸置") なんかを参考に `Send Hex Codes 0x4a` するようにしてみたりしたのだけどうまくいかなかった。

しかし先ほど仕事をさぼって iTerm の設定項目を確認していたら以下の設定で使えるようになったのでここに書き記しておきます。

![iTerm で Ctrl + Shift + J でかな入力変換する方法](/images/iterm-do-not-remap-modifiers.png)

↑のように、iTerm の Preferences -> Profile -> Keys で `Ctrl + Shift + J`、 `Ctrl + Shift + *` の項目を追加し、メニューから "Do Not Remap Modifiers" を選ぶだけでオッケー。かな英数の切り換えが快適に行えるようになる。困っている方お試し下さい。
