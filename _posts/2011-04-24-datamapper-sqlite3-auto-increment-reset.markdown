---
id: 53
title: DataMapperでAUTO INCREMENT値をリセットする
category: Ruby
layout: post
---

ポータルシットをLokkaに置き換えたくていろいろやってる。ポータルシットの過去記事をYAMLでエクスポートし、それをLokkaのDBに取り込む作業をやってる。TDD BootCampに参加したので、テストファーストしながらの作業。RSpecでテストコードを書き、ログが正しくインポートできることを確認する。テスト終了時 `after(:all)` フックで、取り込んだログを削除してる。コードはこんな感じ。ちなみにLokkaはDataMapperをORMに採用してるので以下はDataMapperでの話。

{% highlight ruby %}
after(:all) do
  Category.all.destroy
  Entry.all.destroy
end
{% endhighlight %}

しかしこれでは `AUTO INCREMENT` の値がリセットされず、テストを繰り返す度に `AUTO INCREMENT` の値が増えていってうざかった。

DataMapperの機能で `AUTO INCREMENT` 値をリセットするのってないのかなと5秒くらい探してみたけど見つからなかったので、SQLを直接実行する方法を採用した。

* [DataMapperでSQLを直接実行する - Hello, world! - s21g](http://blog.s21g.com/articles/1408 "DataMapperでSQLを直接実行する - Hello, world! - s21g")

ちなみにRDBMSに採用してるのはSQLite3。SQLiteでは `UPDTE sqlite_sequence SET seq=0 WHERE name='テーブル名';` みたいなコードで `AUTO INCREMENT` 値を任意の値に設定できるみたい。

* [[悪徳商法？支店]: auto_incrementの値を1に戻す方法](http://beyond.cocolog-nifty.com/akutoku/2008/04/auto_increment1_a1f6.html "[悪徳商法？支店]: auto_incrementの値を1に戻す方法")

最終的な `after(:all)` フックはこんな感じ。

{% highlight ruby %}
  after(:all) do
    Category.all.destroy
    Entry.all.destroy
    Entry.repository.adapter.execute('update sqlite_sequence set seq=0 where name="entries";')
  end 
{% endhighlight %}

テスト実行後にはすべてのデータがデータベースから削除されて、`AUTO INCREMENT` の値もリセットされる。1人畜無害なテストコード。
