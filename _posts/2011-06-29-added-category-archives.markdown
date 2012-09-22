---
id: 57
title: Jekyllにカテゴリ一覧を追加した
categories:
- jekyll
- ruby
layout: post
---

Jekyllを使いだしてから気がつくと一年経ってました。いろいろ便利に使えており気に入っております。

PygmentでコードをシンタックスハイライトしたりLSIで関連記事表示したりと結構手を入れてはいたんだけど、いわゆる世間の一般のブログにあるようなカテゴリ一覧表示機能と、カテゴリごとの記事アーカイブ機能がなくて、それを若干不便に思っておりました。

ググってみたところ、プログラマー向けなブログツールなだけあっていろんな方法が出てきました。以下そのまとめ。

### カテゴリ一覧

JekyllのLiquid (テンプレート言語) には `{{ "{{ sites.categories " }}}}` みたいタグがあるんだけど、こいつが意図したとおりに動かない。普通のRuby使いの感覚からすると `site.categories` ってカテゴリを沢山持った配列になってそうな気がするんだけどこれが違う。

{% highlight html linenos %}
<ul>
{{ "{{ for category in sites.categories " }}}}
  <li>{{ "{{ category.name " }}}}</li>
{{ "{{ endfor " }}}}
</ul>
{% endhighlight %}


↑みたいな感じのコード書くと何も表示されない。 `site.categoires` はHashで、`{ "カテゴリ名" => カテゴリ内の記事一覧 }` みたいな構造になってる。LiquidでHashのキーを取りだす方法が分からず、どうにもこうにもいかなかったので他の人が作っているプラグインを利用することにした。

[tag_category_iterator/tag_category_iterator.rb at master from rfelix/my_jekyll_extensions - GitHub](https://github.com/rfelix/my_jekyll_extensions/blob/master/tag_category_iterator/tag_category_iterator.rb "tag_category_iterator/tag_category_iterator.rb at master from rfelix/my_jekyll_extensions - GitHub")

↑のファイルを `JEKYLL_ROOT/_plugins` にコピーする。（`_plugins` というディレクトリがなければ作る）。そんでテンプレートを変更する。↑のやつを↓みたいにする。

{% highlight html linenos %}
<ul>
{{ "{{ for category in sites.iterable.categories " }}}}
  <li>{{ "{{ category.name " }}}}</li>
{{ "{{ endfor " }}}}
</ul>
{% endhighlight %}

2行目のところが変更点です。これでカテゴリ一覧表示ができるようになる。

### カテゴリごとの記事一覧

カテゴリごとの記事一覧を表示する方法だけど、こういうのを発見した。

[Jekyll Plugins - Recursive Design](http://recursive-design.com/projects/jekyll-plugins/ "Jekyll Plugins - Recursive Design")

ここの `generate_categories.rb` を使えばカテゴリ内の記事一覧を作成できる。こんな感じ。

[Category: Ruby \| tech.portalshit.net](http://tech.portalshit.net/categories/Ruby/ "Category: Ruby \| tech.portalshit.net")

これもさっきのと同じように、`JEKYLL_ROOT/_plugins` にファイルをコピーする。そんでLiquidテンプレートを書き換えるんだけど詳細はプラグイン内の記事をご確認くだしあ。
