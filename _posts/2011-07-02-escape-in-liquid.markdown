---
id: 58
title: Liquidの中でLiquidをエスケープする
categories:
- Jekyll
- Ruby
- Liquid
layout: post
---

JekyllはLiquidというRubyのテンプレートエンジンを採用してるんですが、Liquid内でLiquidの文法をエスケープする方法が分からず大変苦しんでおりました。Jekyllの公式のDocument呼んでもXML出力時とかCGI出力時にコンテンツをエスケープする方法は書いてあるのに、Liquidテンプレート自体をエスケープする方法が書いてなく、大変不満でした。しかしその方法が分かったのでお知らせいたします。元ネタはスタックオーバーフロー。

[web development - How to escape liquid template tags? - Stack Overflow](http://stackoverflow.com/questions/3426182/how-to-escape-liquid-template-tags "web development - How to escape liquid template tags? - Stack Overflow")

例えば `{{ "{% this " %}}}` と表示させたかったらこうやります。

<pre>&#123;&#123; "&#123;% this " %}&#125;&#125;&#125;</pre>

ちょっとトリッキーですね。

Pygmentsと組み合わせて使うことも可能ですが、いちいち `{{ "{% highlight " %}}}` のなかでコメントアウト処理をしてあげないといけないません。面倒くさいですね。
