---
id: 56
title: User Streamで快適ネットストーキング生活
category: Ruby
layout: post
---

Twitterで特定のユーザーのことばかりfavっていて不愉快という指摘を受けて頭に来たので、全自動で特定のユーザーを延々favし続けるスクリプトを書いた。

<script src="https://gist.github.com/972943.js?file=favstream.rb"></script>

ヒトデ君が書いた [hitode909/user-stream-receiver - GitHub](https://github.com/hitode909/user-stream-receiver "hitode909/user-stream-receiver - GitHub") と[Ruby+User Stream APIで無言リプライに高速返信するbotを作りました - ps aux \| grep aquarla](http://d.hatena.ne.jp/aquarla/20101020/1287540883 "Ruby+User Stream APIで無言リプライに高速返信するbotを作りました - ps aux \| grep aquarla") を参考にさせてもらった。というかほとんどまるパクリ。またOAuthのところはtily氏の oauth-twitter-cli に全面的に依存している。

User Stremを受診してるのでcronとかの設定なしでネットストーキングしたい相手のことを延々追跡できる。しかも発言があった瞬間に即favする。大変気持ち悪いですね。

しかしUser Streamはときどき調子が悪く、発言を拾い落とすこともある。そんなときは以下のコードを使う。

<script src="https://gist.github.com/972943.js?file=favoritter.rb"></script>

これでUser Stream経由で取りこぼした発言もfavできる。それぞれ使い方はこんな感じ。

{% highlight console %}
  ruby favoritter.rb ストーキングしたい相手ユーザー名
{% endhighlight %}

{% highlight console %}
  ruby favstream.rb ストーキングしたい相手のユーザー名
{% endhighlight %}
