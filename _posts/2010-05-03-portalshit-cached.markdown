---
id: 5
title: ポータルシットにキャッシュを効かせた
category: PHP
layout: post
---


ポータルシットがクソ重くて、なんか対策ないかなーとか仕事をさぼりながらときどき調べてた。

おおよその原因は掴んでいた。それはアクセス解析プラグイン。MySQLのデータ容量がでかくなるとページの表示が遅くなる。アクセス解析プラグインを無効にした状態でページの表示速度はだいたい0.05秒くらいなんだけど、アクセス解析プラグインを有効にすると表示速度は1秒台とかまで悪化する。アクセス解析に使うテーブル（ `p_page_analyze` ）をDROPするとまた速さが回復するので時々空にしていた。

しかしよくよくアクセス解析プラグインのコードを覗いてみると、ヴュー部分で使っていないSQLクエリが発行されており、このせいでクエリの回数が必要な回数の何倍にもなっていた。ポータルシットのアクセスなんて大したことないんだから、DBのサイズがちょっとでかくなっただけでこんなに遅くなるはずがないのだ。

そういうわけで不必要なクエリのトリガーになるコードをコメントアウトしてみた。すると1秒台だった表示速度は0.2秒から0.5秒程度に収まるようになった。しかしそれでもなんか遅く感じる。

それでキャッシュを効かせることにしてみた。使ったのはPecl APC。DreamHostはなんでもやらせてくれるのでほんと助かる。

[Pecl APC - DreamHost](http://wiki.dreamhost.com/Pecl_APC) を見ながらシェルスクリプトをコピペして走らせ、php.iniにAPCの設定を書き加えて終了。僕はPHPのバージョンを5.3.1に上げているのでコピペしたシェルスクリプトのまんまではきちんと入らなかった。最新版のAPC（APC-3.1.3p1）にバージョン情報を書き換えてインストールしたところうまくいった。またDreamHost Wikiではキャッシュファイルのパスが `/home/username/tmp/apc.*XXXXXX*` だったり `/home/username/tmp/apc.*XXXXX*` だったりばらついてるけど、Xの数は6個じゃないと500エラーが出るのでご注意を。

キャッシュを効かせて見た結果、フッターのPage Generationはあまり変化がないが、体感速度は十分に速くなった。