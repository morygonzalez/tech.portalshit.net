---
id: 40
title: CakePHPのMedia Plugin 1.3が動かない
category: CakePHP
layout: post
---

動かしてるサイトのCakePHPのバージョンを最新版の1.3.4に上げようと思って、Media PluginもCakePHP 1.3対応バージョンの1.3alphaにアップデートしようとした。

とりあえず本体を `git clone http://github.com/cakephp/cakephp.git` し、Media Pluginを `git clone http://github.com/davidpersson/media.git` してみた。

Media Plugin 1.3での設定方法とか調べてみようと思って、GitHub上のWikiのページを探すんだけど見つからない。なんと、作者サマはVer 1.3からWikiを消しちゃったみたい！ そんまま動かしてみたところではMedia Plugin動いてないみたい。Mediumヘルパーがないというエラーが出る。結局、プロジェクトの中の `docs` ディレクトリにドキュメントが格納されていたのを発見したので（[docs at 1.3 from davidpersson's media - GitHub](http://github.com/davidpersson/media/tree/1.3/docs/ "docs at 1.3 from davidpersson's media - GitHub")）そこを参考にしながらMedia Plugin 0.6から1.3へのMigration作業をやったんだけど、とうとうできなかった。

まず第一に、クラス名が変わってる。`Media.Medium` だったのが `Media.Media` になってる。Viewファイル内での変数も `$medium` ではなく、 `$media` になってる。そしてメソッドとかもHTML5対応とかで結構変わってるみたい。

さらに、media processing 関連のクラスが分割されて別のライブラリとしてMedia Pluginの中に含まれてる（[davidpersson's mm at master - GitHub](http://github.com/davidpersson/mm "davidpersson's mm at master - GitHub")）。これが結構わかりにくい。なんかImagick必要ぽくて、本番環境じゃインストール権限ないので使えないし、結局ここで諦めてしまった。

RubyのライブラリはたいていRdocとかついててドキュメントが充実してるので、あれに慣れた身からするとドキュメントがわかりにくいライブラリやプラグインは億劫に感じてしまう。