---
id: 19
title: XREAにRubyGemsをインストール
category: Ruby
layout: post
---

XREAでRailsを使おうと思っていろいろ調べてみた。Railsは `rake rails:freeze:gems` してアップロードすればオッケーらしいんだけど、RubyGemsはインストールしないといけないみたい。ところがネットに乗ってる情報を参考にインストールしてみたけど全然うまくいかなかった。指示通りにやってるんだけどパスが通らないのか、インストールしても 'rubygemsをrequireできねーぞゴラ！' みたいなエラーが出る。

`.profile` で記述した `GEM_HOME` や `RUBY_LIB` のパスは間違ってないと思うんだけど、何回やっても `$HOME/lib/` 直下にRubyGems系のファイルが展開されてしまう。これがエラーの原因っぽい。しょうがないので力業で `guantlet_rubygems.rb, rbconfig/ rubygems/ rubygems.rb, ubygems.rb` を `$HOME/lib/ruby/site_ruby/1.8` に移動させた。その後 `source ~/.profile` して適当な場所で `gem -v` してみたところ、ちゃんと `1.3.5` と表示された。

蛇足だけど最初、RubyGems 1.3.7をインストールしようとしたら、利用予定地のサーバーのRubyのバージョンが1.8.5なためにインストールできなかった。そういうわけでRubyGemsは1.3.5を入れた。

あとRubyGemsが入ったからといってシェルで `gem install rails` とかやってもプロセスを `kill` されるっぽいのでよい子のみなさんは必要な gem は自分のパソコンでインストールしてからアップロードした方がよさげです。
