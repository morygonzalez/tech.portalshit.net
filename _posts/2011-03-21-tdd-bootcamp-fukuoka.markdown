---
id: 47
title: TDD Boot Camp福岡に参加した
category: TDD
layout: post
---

昨日と一昨日の二日間、TDD Boot Camp 福岡に参加した。

### 参加しようと思ったわけ

勤めている会社にはテストがない。いや、テストはある。エクセルにテスト項目をたくさん書き出していって手動テストだ。テストコードがない。人力で三人くらいが夜なべしてテストする（だいたいスケジュールには遅延が発生する）。これはどうしたっておかしい。開発前に要件定義書、設計書を書いて開発して、開発が終わったらエクセルで長大なテストシートを作成し、手動テストを行う。そしてバグや思わぬ不具合が発見されるとプログラムに改修を加える。欠陥や不都合が発見される度に連動して設計書にも修正・変更が加えられ、Do Repeat Yourselfな感じになってる。毎日毎日ドキュメント作成などの開発以外のタスクに時間を割かれるので新しい技術に触れる機会がないし、遅くまで残って仕事してから帰宅するので趣味プログラミングで知見を広めることもできない（福岡に来てからのこのブログの更新状況を見ればおわかりいただけるかと）。この状況をなんとかしたいと思っていて、藁をもすがる思いでTDD Boot Campに参加した。

### 感想

一日目は『プログラマが知るべき97のこと』の監修やTDDで有名な [@t\_wada](http://twitter.com/t_wada) さんのレクチャーで、TDDとは何かが説明された。以下印象に残った点。

- 良いテスト
  - 自動化されている
  - 徹底している
  - 何度でも実行可能
  - 独立している
  - プロのコード
    - テストコードもプロダクトコードと同じ品質であることが求められる（リファクタリング、DRY原則の貫徹など）
- TDD三原則
  - 単体テストコードを書く前に製品コードを書いてはいけない
  - 適切に失敗する単体テストコードができるまで、次の単体テストコードを書いてはならない
  - 単体テストコードに対応する以上に製品コードを書かない
- なぜTDDするのか
  - 自分が完璧ではないことがわかっているから
    - 最初から思い通りにコードを書けるほどに私たちは賢くない
    - 最初から思い通りに動作するほど対象は単純ではない
    - 素早く対象に近づき、フィードバックを得て方向修正をしながら開発を行う必要がある
- テストの目的は健康
  - 変化に対応できるのは健康体のコードだけ
  - 変化に対応できるのは健康体のチームだけ
    - 毎日残業する、毎日レッドブル飲んだりしていてはダメ
- TDDの導入効果
  - MSやIBMでTDD導入後、欠陥の割合が4割から9割削減された。
  - コード実装時間は15%から35%増加した。
    - しかし結果的にはバグが激減するので開発工数自体は減る。
- TDDは才能ではなくスキル
  - 練習すれば習得可能
  - 量は質に転化する
  - 写経しましょう！
    - PCにGitをインストールし、ページをキープできるブックスタンドを買って、ケント・ベック本をひたすら写経。ビルドを実行する度にコミットする。

テストのみならず、自動化やバージョンコントロールの重要性が説かれた。

二日目には [@bleis](http://twitter.com/bleis) さんによるGitの効果的な利用方法やJenkinsを利用した継続的インテグレーションの実践例、 [@akineko](http://twitter.com/akineko) さんによるOMakeを利用した自動ビルド、自動テスト、自動コミットの話など。

### ペアプログラミングを体験した

ペアプログラミングを生まれて体験した。 [@mallowlabs](http://twitter.com/mallowlabs) さんとRubyでペアプログラミングをさせてもらった。講師陣が出題する課題を解いていくというもの。当然テスト駆動。テスティングフレームワークにはRSpecを利用した。

WEB + DB PressなどのRSpec特集を写経したことはあったけど、時間制限がある中で、他の人とペアを組んでプログラムを書いていく作業はかなりエキサイティングだった。

ただ自分のRubyスキルおよびVimのスキルが著しく劣っていたため、@mallowlabs さんの足を引っ張っていた感は否めない。正直申し訳なかったです。

全般的に、自分の知識のなさ、スキルのなさが実感できた

以下、初日に行ったFizzBuzz問題と主に二日目に取り組んだTwitterのタイムラインをカテゴリ分けするという課題の成果物。

[TDD Boot Camp 福岡 — Gist](https://gist.github.com/879647)
[TDDBC でペアプロした結果です — Gist](https://gist.github.com/878159)

### TDDをいかにして根付かせるか

勉強会に参加していきなりコードが書けるようになるわけでは当然ないので、継続的な勉強が必要だと感じた。いっぱい本を紹介してもらったので積ん読本を何冊か片付けたら『レガシー・コード改善ガイド』と『テスト駆動開発入門』を買おうと思った。
