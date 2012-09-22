---
id: 64
title: Railsで `building` って予約語なんすかね
category: Rails
layout: post
---

Railsで建物名みたいなカラムに `building` ってのを当ててたら

{% highlight ruby %}
ActionView::Template::Error (no block given (yield)):
{% endhighlight %}

みたいなエラーが出るんですけど、Railsで `building` って予約語なんですかね。

なんか Rails Wiki の[Reserved Words You Can’t Use](http://wiki.rubyonrails.org/rails/pages/reservedwords "Reserved Words You Can’t Use => Rails Wiki") は真っ白だし、古い方のWikiの[予約語一覧](http://oldwiki.rubyonrails.org/rails/pages/ReservedWords "ReservedWords in Ruby on Rails") にも `building` は入ってないし。

とりあえず複数形にして対応したけど気持ち悪い。

### 追記

どうやらMongoidに起因するエラーのようです。

[[#RUBY-338] no block given (yield) - MongoDB](https://jira.mongodb.org/browse/RUBY-338 "[#RUBY-338] no block given (yield) - MongoDB")
