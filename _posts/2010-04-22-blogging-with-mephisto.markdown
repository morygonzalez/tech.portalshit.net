---
id: 1
title: Mephistoで技術ブログをやることにした
layout: post
category: misc
---


なんかTwitterで「最近のポータルシット変わったよね…」とかいう意見を目にするようになったので、パソコンネタだけ隔離して別にブログを始めることにした。使っているCMSはMephisto。Railsの勉強になるかと思って。早速DreamhostへMephistoをインストールしていて躓いてしまったのでちょこっとメモ。

とりあえず tech.portalshit.net というサブドメインを用意し、DreamhostのパネルでPassengerのセットアップ。その後SSHでサーバーに接続し、

{% highlight console %}
    $ git clone git://github.com/emk/mephisto.git
{% endhighlight %}

してgithubからプロジェクトをclone。

Mephistoのインストールにはいくつかgemが必要。Dreamhostには結構たくさんgemがインストールしてあるんだけど、いくつか足りないものがあった。とりあえず設置ディレクトリのルートで

{% highlight console %}
    $ rake gems:install
{% endhighlight %}

と打ってみたところ、nokogiriとそれに依存するbrynary-webratが入らなかった。原因を調べてみたところ、xsltのライブラリをダウンロードして、`gem install` するときにパスを指定してあげる必要があるらしい。xsltのライブラリ自体はPHP5をカスタムインストールしたときに入れてあるので、以下のオプションでインストールした。

{% highlight console %}
    $ gem install nokogiri \
    --with-xslt-include=/home/morygonzalez/php5/include/ \
    --with-xslt-lib=/home/morygonzalez/php5/lib/
{% endhighlight %}

無事インストール成功。その後もう一回 `rake gems:install` を実行してbrynary-webratも入り、管理ページにアクセスしてみると今度はPassengerのエラーが。これは単純にdatabase.ymlに `development:` のDB環境しか記述していなかったこと、 `rake db:bootstrap` のときに `RAILS_ENV=production` をつけていなかったことが原因だった。そういうわけでdatabase.ymlに `production:` の設定（sqlite3を使用）を書き、

{% highlight console %}
    $ rake db:bootstrap RAILS_ENV=production
{% endhighlight %}

ですべてのインストール作業完了。いまこうして動いております。

今後はここにCakePHPやRails、JavaScript関連のことを書いていこうと思います。できれば一日一ポスト、その日に学んだことを書いていきたいです。
