---
id: 28
title: Gitのhookを使ってDreamhost上のJekyllに記事を公開
categories:
- Jekyll
- Git
layout: post
---

やってみた。以下を参考にした。

[Deploying a jekyll generated site](http://www.taknado.com/en/2009/03/26/deploying-a-jekyll-generated-site/)

これもうむかし.macとかについてたiBlogとかわらんわ。GUIのクライアントはないけど、VimとかCodaとか好きなエディタ（TextMateで日本語がネイティブに扱えたらなー）で記事書いて、gitで `git push` するだけ。

で、やり方なんですけどちょっとgitに慣れてない人には複雑かもしれない。三つgitのリポジトリを用意する必要がある。

まず記事を作成するパソコンでgitとjekyllのセットアップをしたあと、リポジトリを作る（リポジトリ1）。その後Dreamhostの公開ディレクトリでないところに空のリポジトリを作る（ `git --bare init` ）。ここでは `blog.git` という名前にしましょう（リポジトリ2）。そんでそこにリポジトリ1をpushする。その後リポジトリ2の `/blog.git/hooks/` に `post-update` というファイルを作り、以下のように書く。ファイルに実行可能なアクセス権を与えることを忘れずに。

{% highlight bash %}
    #! /bin/sh
    unset GIT_DIR && cd $HOME/tech.portalshit.net/ && git pull
{% endhighlight %}

そんでもって `git clone blog.git <公開用のディレクトリ名>` する（リポジトリ3）。リポジトリ1から公開用ディレクトリにリポジトリがコピーされるので、この中に含まれる `_site` というディレクトリを panel.dreamhost.com で公開ディレクトリとして設定すると、`git push` する度にhookが発動されて、めでたく記事が公開されるという次第です。

### まとめ

まとめると、

1. 記事を作成するローカルリポジトリ
2. ローカルリポジトリをpushするリモートリポジトリ
3. リモートリポジトリをcloneする公開用リポジトリ

の三つが必要なことを忘れないようにしてくだしあ。

これであなたもハイド博士だ！
