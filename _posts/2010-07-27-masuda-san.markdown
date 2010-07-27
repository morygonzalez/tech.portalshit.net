---
id: 31
title: 増田のRSSをRubyのRSS:ParserでParseしようとしたけどやらせてもらえなかったのでHpricotを使った話
categories:
- Ruby
- bot
layout: post
---

[@ningengasinu](http://twitter.com/ningengasinu) 様みたいに、自分で作ったボットに「日記書いた」ってしゃべらせようと思って、増田のRSSを使わせてもらおうと思ったんだけど、Rubyの `RSS::Parser` で読み込もうとすると500 Internal Server Errorが返ってきてしまう。ブラウザから読み込むときはエラーとか出ないんだけど。

しょうがないので `open-uri` を使って `User-Agent` を偽装してRSSを読みに行ったところ、正しくレスポンスが返された。しょうがないので `RSS::Parser` は使わず、 `Hpricot` を使った。

増田ってbotのアクセス弾いてるんですね。これがネットの闇ですか……