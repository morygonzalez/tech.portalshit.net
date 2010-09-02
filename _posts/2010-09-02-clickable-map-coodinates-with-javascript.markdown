---
id: 38
title: JavaScriptでClickable Mapの座標を取得する
category: JavaScript
layout: post
---

みなさん、クリッカブルマップしてますか？ あんなくそみたいなもの使って地図をつくるなんて発狂しそうなこと、ここを読みそうな人はやってないと思いますが、僕の職場のお客さんとか上司は「Google Mapsには心がこもってない」とか言うので、クソみたいイラストをクリッカブルマップにして地図を作ってるんですよ。まじでかわいそうな僕ちゃん。

ご存じない方のためにクリッカブルマップの作り方を説明しておくと、まず画像を作り、それをHTMLに貼り付け、HTMLオーサリングツール（うちの職場ではDreamWeaver）のGUIエディタでちまちま画像上のクリッカブルにしたい位置を選択するという、血尿が出そうなくらい面倒くさい作業を強いられます。

最悪なことにこのクリッカブルマップのあるページ、頻繁に更新依頼が来るのですよね。依頼が来る度に就業時間中の快適なネットサーフィンが妨げられるので、一発JavaScriptを書いて画像上の座標を取得することにしました。いちいちクソみたいに重いAdobe DreamWeaverとか立ち上げてられるか。

コードはこんな感じ。

{% highlight html %}
<html>
  <head>
    <script>
      function getPosition(){
        var x, y;
        var image = document.getElementById('image');
        image.onclick = function(e) {
          x = e.layerX;
          y = e.layerY;
          document.getElementById("pointX").value = x;
          document.getElementById("pointY").value = y;
        }
      }

      window.onload = getPosition;
    </script>
  </head>
  <body>
    <div>
      <img src="path/to/image" id="image" style="position: absolute; top: auto; left: auto; width: 500px; height: 332px" />
    </div>
    <form action="/" method="post">
      <input type="text" id="pointX" name="pointX" value="" />
      <input type="text" id="pointY" name="pointY" value="" />
      <input type="submit" value="発射！" >
    </form>
  </body>
</html>
{% endhighlight %}

Firefoxでしか動作確認してないけど多分IEでは動かないと思います。ここのサイトを参考にさせてもらいました。

[座標取得するプロパティのそれぞれの違い - 三等兵](http://d.hatena.ne.jp/sandai/20091105/p1 "座標取得するプロパティのそれぞれの違い - 三等兵")
