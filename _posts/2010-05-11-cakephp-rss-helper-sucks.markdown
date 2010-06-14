---
id: 9
title: CakePHP 1.2.xのRSSヘルパーはわかりにくい
categories:
- CakePHP
- Ruby on Rails
layout: post
---

ちょっとCakePHPで作ってるサイトでRSSフィードを配信したいと思ったのでやってみたんだけど、思いの外面倒くさくてびっくりした。『RailsによるアジャイルWebアプリケーション開発』を読みながらRails 2.3.5でRSSフィード作るときは結構簡単だった気がするので、正直これはないわと思った。

『Railsによる〜』で作ってるデモプロジェクトのdpeotのコードを見てみると、RSSを配信するときはControllerに以下のように記述し、

<pre><code>
    respond_to do |format|
        format.html # index.html.erb
        format.xml  { render :xml => @products }
    end
</code></pre>

`config/routes.rb` に

<pre><code>
    map.connect ':controller/:action/:id.:format'
</code></pre>

と書いたあと、RSS用のViewを用意してやるだけだ。ものすごくシンプルで簡単だった。

CakePHPで同じことをやるためには以下の手順が必要。

[Creating an RSS feed with the RssHelper :: RSS :: Core Helpers :: The Manual :: 1.2 Collection :: The Cookbook](http://book.cakephp.org/view/483/Creating-an-RSS-feed-with-the-RssHelper)

ちょっと面倒くさすぎてやる気にならなかった。どうせいま僕が作ってるサイトなんてRSSリーダー使うような人が見るサイトじゃないし、フィード配信機能の実装はそんなにプライオリティ高くないので他にやることがなくてどうしようもなく暇なときにでもやろう。

Railsは最初のとっかかりのハードルは高いけど、使い方を覚えていったらやっぱりCakePHPとかよりも全然簡単かつ高速に開発できる気がする。レールに乗ってる感強い。このMephistoの設置もすごく楽だった。ただTerminalを使い慣れた人や、サーバーにSSHでアクセスできる環境じゃないとRailsアプリケーションを使うのは難しい。CakePHPは反面、全部FTPでアップロードすれば良いのでサーバーに標準的な構成でPHPがインストールされてりゃ環境構築でつまずくことはない。どっちをとるかって話ですよね。

僕はファッションの観点からRailsを選びたい。