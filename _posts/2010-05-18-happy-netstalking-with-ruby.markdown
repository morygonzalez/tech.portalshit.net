---
id: 11
title: たのしいネットストーキング with Ruby
categories:
- Ruby
- Twitter
layout: post
---

この前大阪で第二回アメ村ブルゾンの会をやったんですけど、そこで日夜<del>ネットストーキング</del>プログラミングにいそしんでおられる皆さんとお会いして、TwitterのStreaming APIの使い方を教えてもらいました。なんか自分でやろうとしてたんだけど、全然見当違いなところを見ていたみたいで、僕もStreaming APIでネットストーキングできるようになりました。pokutunaさんにもらったコードと "Twitter Streaming APIをRubyで試してみる - しばそんノート":http://d.hatena.ne.jp/shibason/20090816/1250405491 を参考に、以下のような感じにしてみました。

<pre><code>
#!/usr/bin/env ruby
# coding: utf-8

require 'net/http'
require 'uri'
require 'rubygems'
require 'json'

USERNAME = 'morygonzalez'
PASSWORD = '***'

uri = URI.parse('http://chirpstream.twitter.com/2b/user.json')
begin
  Net::HTTP.start(uri.host, uri.port) do |http|
    request = Net::HTTP::Get.new(uri.request_uri)
    request.basic_auth(USERNAME, PASSWORD)
    http.request(request) do |response|
      raise 'Response is not chunked' unless response.chunked?
      response.read_body do |chunk|
        #空行は無視
        status = JSON.parse(chunk) rescue next
        #eventを含まないものは無視
        next unless status['event']
        source = status['source']
        if status['target_object']
          target_obj = status['target_object']
          target_user = target_obj['user']
          puts "#{status['event']}: #{source['screen_name']} -&gt; #{target_user['screen_name']}: #{target_obj['text']}"
        elsif status['target']
          target = status['target']
          puts "#{status['event']}: #{source['screen_name']} -&gt; #{target['screen_name']}"
        end
      end
    end
  end

rescue Timeout::Error => ex
  p "&lt;-----!!!! Timeout::Error!!!!-----&gt;"
  
  retry
end
</code></pre>

教えてもらったコードではTweetの内容を垂れ流しにするやつだったんですけど、自分でちょこっといじってTweet以外のステータスを表示するようにしてみた。しかしなんか調子悪いっぽくて、完全にはStreamを取れてないっぽいです。

でもまぁ一歩前進したことは確か。Rubyがんばるぜ。