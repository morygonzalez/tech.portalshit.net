---
id: 18
title: CakePHPはSchemaとかがしょぼいしうんざりする
category: CakePHP
layout: post
---

CakePHPで作ってたプロジェクトのDBのフィールド名にスペルミスを発見したので（ `longitude` を `longtitude` としていた）、それを修正するためにDBの構造をいじった。このとき、Cakeは普通にやってたらSchemaとかの概念に触れる機会がないことに気がついて急に怖くなった（ここんとこRailsばっかり触っていたので）。いや、CakePHPにもSchemaの概念はあるんだけど、普通にサイト作るだけだったら世話になる機会がない。というか俺がCakeの底本にしてた公式ガイドにSchemaの項目がない！

これじゃあgitとかでバージョン管理しててもDBの論理構造が置いてけぼりになって、分散管理とかできないじゃん。SQLite使ってたらバイナリファイルをgitでtrackすればまぁ分散開発でけそうだけど、MySQLとかだったら死ぬよね。

確かにCakePHPでサイト作るのは楽だったし早かった。ほぼ何もできない状態の自分が数ヶ月でCMS作れたのはCakePHPのおかげなんだけど、CakePHPは何でもテケトーな感じがする。対してRailsは厳格だ。楽するためのフレームワークというより、よりStrictにサイトを構築するためのフレームワークという感じがする。だから慣れるまでは時間がかかる面があるのは否めないんだけど、SchemaにしろTestにしろ、Railsやってて勉強になることはたくさんあります。はやく皆と同じようにrailsの手術を受けたい。