---
id: 44
title: AutoPagerizedなページでもJavaScriptを動かす
categories:
  - JavaScript
  - jQuery
layout: post
---

あけましておめでとうございます。なんか2011年後半は転職とか引っ越しとかあってあまりここに記事を書けなかったのが残念です。Rubyとか全然さわってねーし、JavaScriptも忘却曲線の彼方。というわけで2011年一発目はJavaScriptについて。

AutoPagerize対応なページで、読み込まれた2ページ目以降でもJavaScriptを動かす方法について調べてみた。oAutoPagerizeのos0xさんのページでまとめられてる。

[AutoPagerizeで継ぎ足された部分に自分のスクリプトを適用する方法あれこれ - 0xFF](http://d.hatena.ne.jp/os0x/20090829/1251556449)

いちばん手っ取り早そうだったので、以下のような書き方をした。

{% highlight javascript %}
if (window.AutoPagerize) {
  window.AutoPagerize.addFilter(fucintion(){
    // 実行したい処理
  });
}
{% endhighlight %}

ただ無名関数は呼び出せないので、二回書かなければならなくなる。これはアホっぽい。関数リテラルにして呼び出し用に `function init()` みたいのを書き、その中から呼び出せばよい。そしてその `init()` を上記 `// 実行したい処理` 内にも書いてあげればオッケーだ（もちろん `window.onload` で呼び出す必要もある）。

jQueryについては `live()` というメソッドがある。これは動的に生成された要素にもスクリプトに適用してくれる非常にありがたいメソッドだ。しかし個人的な事情で、 `live()` というメソッドと一緒に、処理を一度しか実行しないというメソッド `one()` も適用している要素があり、これを二つ両立するのがjQuery的に無理っぽい。単純に処理実行のフラグを作って処理を分ければいいんだけど、これにもjQuery的なかっこいい書き方があることを知った。ネタもとはこちら。

[Using .one() with .live() jQuery - Stack Overflow](http://stackoverflow.com/questions/3796207/using-one-with-live-jquery)

{% highlight javascript %}
$('処理を適用したい要素').live('click', function(e) {
  if($(e.target).data('oneclicked')!='yes')
  {
    //Your code
  }
  $(e.target).data('oneclicked','yes');
});
{% endhighlight %}

`jQuery().data()` 、なかなか便利そうだ。