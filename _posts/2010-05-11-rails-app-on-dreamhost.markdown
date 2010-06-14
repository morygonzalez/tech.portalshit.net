---
id: 10
title: DreamHostでRailsアプリケーションを再起動
categories: Ruby on Rails
layout: post
---

レンタルサーバーみたいな共有サーバーとか `sudo` 権限のないサーバーで動かしてるRailsアプリケーションを再起動したくなることがある。でもApacheをリスタートする権限がない。じゃあどうするかとググっていたらこういう記事にたどり着いた。

> To restart your rails app do a "ps x" to get the pid of your dispatch.fcgi process(let's say it's 1234) then do a "kill 1234". This will kill the running process and a new one will be automatically spawned and you should now see your changes. 
> <cite><a href="http://forum.dreamhosters.com/3rdparty/77334-How-do-I-restart-rails-app.htm">How do I restart rails app? - DreamHost Forum</a></cite>

要するに `ps x` でRailsアプリケーションのプロセスIDを調べ、 `kill #pid` しちゃうというわけ。 `kill` できんのかなと半信半疑だったけどちゃんとできた。

他のレンタルサーバーには当てはまらないかもしれないけどメモっときます。