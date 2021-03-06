---
id: 14
title: RailsのMVC間の命名規約
categories:
- CakePHP
- Rails
layout: post
---


ポータルシットに前も書いたけど、CakePHPの命名規約ではDBにusersというテーブルがあれば、モデルクラスにUser、コントローラークラスにUsersController、viewsディレクトリにusersっていうのが存在するのを前提とする。これに慣れてしまっているので、Railsのやり方にはなんか慣れない。ModelでPeople、コントローラーでUsersControllerとしてても問題ナッシングなわけだ。むしろRailsではこういうのが普通？ Rails使っててCakeをちょこっと触った人のブログにこういう感想があった。

<blockquote cite="http://rails.takeda-soft.jp/blog/show/190" title="Blog-side CakePHP わかりずらい３点">
<h3>コントロールとモデルが密すぎる。</h3>
<p>CakePHPは、コントロール名とモデル名が密接すぎる関連を持っています。PostsControllerというコントロールを作ったら、必ずPostというモデルが存在しないと「モデルが見つからないエラー」になる。</p>
<cite><a href="http://rails.takeda-soft.jp/blog/show/190" title="Blog-side CakePHP わかりずらい３点">Blog-side CakePHP わかりずらい３点</a></cite>
</blockquote>

ふむふむ〜、ナルホディウスですぞ〜！！！

確かにCakePHPはモデルとコントローラーがガチガチになってて、あるコントローラーが他のモデルクラスにアクセスするときはいちいち

{% highlight php %}
$use = array("Hoge");
{% endhighlight %}

とかしなきゃいけなかった。

最初の頃はモデル、コントローラー、ビューですべてが一対一に対応してるのですんなりMVCの流れを理解できたんだけど、今にしても思えばこういう考え方はすべてのコントローラーに対応するモデル（つまりDBテーブル）がなければならないというしがらみというか束縛を生じさせる。これでは自由な発想で開発できないし、下手をすると一つのコントローラークラスに大量にメソッドを書いてしまったりして、非常にメンテナンス性の良くないコードを量産してしまう公算がある。本当は機能ごとに細かくクラスは分けた方がいいはずだし、メソッドが一つしかないコントローラークラスがあっても良いはずだ。

そういうわけで、はやくこの辺のCake流の思い込みを排除して皆と同じようにrailsの手術を受けたいです。