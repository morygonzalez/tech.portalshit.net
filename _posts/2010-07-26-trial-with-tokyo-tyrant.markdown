---
id: 30
title: Tokyo Tyrantでvalueに配列を保存したらダメなのかしら
category: Ruby
layout: post
---

tilyさんのgist[gist: 427398](http://gist.github.com/427398 "gist: 427398")を使わせてもらってTwitterのボットを何個か作ってみた。結構楽しいですね。

しかしボットが短時間に何度も同じ発言を繰り返してフバいので、日付が変わるまでは重複発言をしないようにしてみようと思った。Rubyは 配列 - 配列 みたいなエロいことができるみたいなので、

    new_tweets = neta_tweets - used_tweets
    
とかしてみようとした。

[gist: 427398](http://gist.github.com/427398 "gist: 427398")自体がTokyo Tyrantを使っているので、これでなんとか出来ないかなと思った。しかし `rdb.put` しようとすると、 `ArgumentError` というのが発生してしまう。ひょっとしたらTokyo Tyrantって配列とかを保存するもんじゃないのかな。