---
layout: post
category: Jekyll
title: Jekyll のデプロイ手順を改めた
date: 2012-09-22 11:15:50
---

だいぶ前の記事では Jekyll は Git の hook を使って公開してると書いてた。

[Gitのhookを使ってDreamhost上のJekyllに記事を公開 \| tech.portalshit.net](http://tech.portalshit.net/2010/07/14/deploy-with-git-hook/ "Gitのhookを使ってDreamhost上のJekyllに記事を公開 \| tech.portalshit.net")

しかし記事の本数が増えてくると、 `jekyll` コマンドで生成した静的なファイルも Git でトラックするのがだるいと感じるようになった。ので Rakefile に以下のような task を追加して、公開先のサーバーに rsync でファイルを転送するように変更した。

{% highlight ruby %}
desc "Publish"
task :publish do
  path = File.expand_path("_site")
  if system("rsync -avz --delete #{path}/ portalshit:sites/tech.portalshit.net/_site/")
    puts "Your blog was successfully published!"
  else
    puts "Something went wrong..."
  end
end
{% endhighlight %}

だいぶデプロイが手軽になった。
