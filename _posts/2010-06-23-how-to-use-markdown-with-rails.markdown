---
id: 20
title: RailsアプリケーションでMarkdownを使う
categories:
- Ruby
- Rails
layout: post
---

RailsアプリケーションでMarkdownを使いたと思った。（Markdown大好きっ子なので）

調べてみたところ、 [BlueCloth](http://deveiate.org/projects/BlueCloth "BlueCloth") というライブラリを使うといいらしい。

これはRailsのプラグインではないのでgemでインストール。

    sudo gem install bluecloth

その後viewで

    <%= markdwon(@item.text) %>

とか書けばいい。

しかしなんも設定しない状態だとRailsアプリケーションはBlueClothを読み込まないので、config/environment.rbに

    config.gem "bluecloth"

と書いてやる。するとめでたくMarkdownが使えるようになる。
