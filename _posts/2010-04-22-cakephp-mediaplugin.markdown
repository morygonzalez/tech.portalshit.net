---
id: 2
title: CakePHPのMedia Pluginは神だけど設置が面倒
category: CakePHP
Layout: post
---


CakePHPには [Media Plugin](http://github.com/davidpersson/media) というのがあって、これがすこぶる便利。画像や文書の他に、動画ファイルまで扱うことができる。PHPではファイルアップロードのところにセキュリティリスクが潜んでいそうなイメージだし、自分のような素人に毛が生えたようなレベルの人間は素直にこういう便利なプラグインを使った方がいい。

しかしこのMedia Plugin、設置が少々面倒だ。情報も英語のものも含めて少ない。僕は二つのプロジェクトでこのMedia Pluginを使ったけど、とても設置に苦労した。はまるポイントはいくつかあるんだけど、今日はDBについて書いておこうと思う。

Media Pluginは `attachments` というテーブルをつくり、ここにファイルのメタデータを格納していく。これはアプリケーションのルート（ `APP` ディレクトリ）で `cake media init` というコマンドをTerminalで打ってやると（ただし `/cake/console` にパスを通しておく必要あり）、Bakeのときのような画面が出てきて初期設定をやってくれる（ `app/config/database.php` の情報にあわせてテーブルも作ってくれる）。しかしCakePHPのデフォルトDBがMySQLであるためMedia PluginもMySQLを想定しているのか、 `app/plugins/media/config/sql/media.sql` のSQL文を単純に実行してしまうと不具合が生じる。実は僕はここで結構はまってた。僕は全部のプロジェクトでSQLiteを使っているので、単純にこのSQLを実行すると、 `attachments.id` のデータ型が `INT(10)` とかになってしまい、エラーに遭遇し続けることになってしまった。SQLiteの場合、idカラムのデータ型は `INTEGER` でなければならないのだ。

これはMedia Pluginに限らないけど、Convention Over Configuration なフレームワークを使うときは、DBのテーブル名に注意をはらわなければならない。否、先にも書いたとおりそれだけでは不十分で、さらにカラムのデータ型とかも規約に沿ったものにしないと、原因不明の謎のエラーに遭遇して開発が停滞する。おっちょこちょいな人（僕も含めて）はその辺の基本的な部分をおろそかにしない方がいいと思った
