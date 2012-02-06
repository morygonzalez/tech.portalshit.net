---
layout: post
category: Git
title: Git flow のベストプラクティスが知りたい
date: 2012-02-06 22:43:11
published: false
---

Git flow を導入して仕事してる。master ブランチと develop ブランチをベースに、 feature ブランチ、hotfix ブランチ、release ブランチをつくって色々やるあれ。確かに便利何だけどだるいところもある。

#### hotfix ブランチのバージョン番号

たとえば誰か（A さんとしよう）がバグを見つけて hotfix を start したとする。hotfix 用のタグを 1.0.1 としよう。

{% highlight console %}
$ git flow hotfix start 1.0.1
{% endhighlight %}

ここで別の誰か（B さんとしよう）が他のバグを見つけたとする。このとき B さんは A さんがローカル環境で 1.0.1 のタグを既に使っていることを知らない。ので当然 `$ git flow hotfix start 1.0.1` してしまう。そんで B さんが
