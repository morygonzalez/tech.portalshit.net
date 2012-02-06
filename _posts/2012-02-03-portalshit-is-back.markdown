---
layout: post
category: Ruby
title: Lokka 用の Capistrano deploy.rb
date: 2012-02-03 21:30:46
published: false
---

Unicorn の設定をミスって（たと思ってけど実はそうじゃなかった）ポータルシットが12月の半ば頃から死んだままになってた。きっかけは Capistrano の導入で、仕事で Capistrano 使っていて大変便利なので、これをポータルシットでも使おうとした。

Unicorn で便利なのが、 `kill -USR2 `cat tmp/pids/unicorn.pid` ` とかやることで、ダウンタイム無しに Rails アプリケーションを再起動できるとこだ。これを Sinatra 製の Lokka でも実現したかった。Capistrano と併せて運用することで、サーバーに SSH で接続せずとも

{% highlight console %}
bundle exec cap deploy:restart
{% endhighlight %}

とかで Lokka を再起動できるようになる。

これまで Lokka の database.yml に DB への接続情報をべた書きしていたのをやめ、起動時にはシェルで以下のコマンドを実行するようにした。

{% highlight console %}
env DATABASE_URL=path/to/db bundle exec unicorn -c config/unicorn.rb -D -E production
{% endhighlight %}

Capistrano の `deploy.rb` に書くと以下のようになる。

{% highlight ruby %}
namespace :deploy do
  task :start do
    run "cd #{current_path}; env DATABASE_URL=#{db_path} bundle exec unicorn -c config/unicorn.rb -D -E production"
  end
end
{% endhighlight %}
