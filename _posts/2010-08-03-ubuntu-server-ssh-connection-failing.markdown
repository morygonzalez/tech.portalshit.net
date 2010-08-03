---
id: 32
title: Ubuntu ServerにSSH接続しようとして "Permission denied (publickey)." が出る
category: Ubuntu
laytou: post
---

NECの安サーバーを買ってサーバーを作ってるんですけど、SSHでエラーが出て困ってます。OSはUbuntu Server 10.04.1 LTS。

まずSSHのおさらいを。クライアント側で

  $ mkdir -p .ssh
  $ ssh-keygen -t rsa （以下略）
  
したのち、サーバー側の `/etc/ssh/sshd_config` の `PasswordAuthentication` を `on` にし、パスワードでSSH接続できるようにして

  $ scp id_rsa.pub username@hoge.com:.ssh/authorized_keys
  
するか、あるいはUSBフラッシュメモリで鍵をサーバーに移す。その後サーバー側で `.ssh/` と `.ssh/authorized_keys` のパーミッションをそれぞれ700と600に変えてあげるわけですよね。

いっぺんクライアント側で `id_rsa.pub` を作ってたらそれ以降は単純にこれを接続先のサーバーにコピーしてあげればおｋ。ここまで合ってますかね？

前から使ってる職場内だけで使うサーバーにも同じUbuntu Serverを入れてるんですけど、こっちでは全くトラブルがない。それなのに新しいサーバーでは

  Permission denied (publickey).

というエラーが頻繁にお出になるのですよ。

しかしこのエラー、常に出る訳じゃないんですね。サーバーを直接操作して

  $ sudo /etc/init.d/ssh restart
  
してあげると消える訳ですね。そんでしばらくクライアントからSSHで接続したり切断したりを繰り返していると、あるとき突然、

　Permission denied (publickey).

となるわけです。まじでストレスフル。つか、このサーバーは公開用に使うものなので、こんな感じでSSHが不安定だとかまじで困るんですけど。

前述の `PasswordAuthentication` を `on` にしとけば、公開鍵認証に失敗した後もパスワードで認証することができるんですが、パスワード認証はなんだか怖いので使いたくないのですよね。どいうしたものか。

ググったらSSHのプロトコルを1と2併用にしたら解決するという情報が出てきたのですけど、これやったら "Disabling protocol version 1. Could not load host key" というエラー？が出てしまったので多分僕の環境では意味なし。「RSAキーやめてDSAにしたらエラーでなくなった」（[ぷらぷらブログ | OpenSSH を導入。接続に四苦八苦！](http://miyazaki.ddo.jp/mt3/blog/zaurus/20060405-2343.html "ぷらぷらブログ | OpenSSH を導入。接続に四苦八苦！")）という情報もあるけど面倒くさいのでまだ試していません。