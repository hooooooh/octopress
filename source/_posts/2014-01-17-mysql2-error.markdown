---
layout: post
title: "MySQL2 Errorが出るよ"
date: 2014-01-17 13:36:14 +0900
comments: true
categories: 
---
すごく初歩的なのだろうし、間違っているトコもありそうだけど…。    

Railsプロジェクトを作成する時に、MySQLを使うって事にすると  
エラーを出してしまって、はっとすることがあるのでメモします。    


##1　DBをMySQLに指定して、プロジェクト作成
    bundle exec rails new test_mysql_project -d mysql

##2　プロジェクトに移動
    cd test_mysql_project


##3　gemをインストール
    bundle install


##4　起動
    bundle exec rails s


##4　MySQL2 Errorのエラーになる(>_<)
    /Users/XXXXX/test_mysql_project/vendor/bundle/gems
    /mysql2-0.3.14/lib/mysql2/client.rb:67:in 
    `connect': Can't connect to local MySQL server through socket 
    '/tmp/mysql.sock' (2) (Mysql2::Error)

socket'/tmp/mysql.sock'を通じてローカルのMySQLサーバーに  
接続することが出来ませんという意味のエラーになります。  
[http://www.hi-ho.ne.jp/tsumiki/book_sup2.html](http://www.hi-ho.ne.jp/tsumiki/book_sup2.html)
に詳しく書いてありました。  
MySQLは起動している前提ですので、パスを指定していない、間違っていることがわかりました。    


##5　config/database.ymlを修正する
socket:のところをなおします。
    development:
      adapter: mysql2
      encoding: utf8
      reconnect: false
      database: test_mysql_project_development
      pool: 5
      username: XXXX（設定したやつ）
      password: XXXX（設定したやつ）
      host: localhost
      socket: /Applications/MAMP/tmp/mysql/mysql.sock（環境にあわせる）

test用、production用の定義もあわせてなおします。


##6　ふたたび、MySQL2 Errorのエラーになる

    /Users/XXXXX/test_mysql_project/vendor/bundle/gems/
    mysql2-0.3.14/lib/mysql2/client.rb:67:in 
    `connect': Unknown database 'test_mysql_project_development' (Mysql2::Error)

DB作成してないよという意味のエラーになります。

##7　DBを作成
以下のコマンドでdatabase.ymlに書いたDBが作成されます。
    bundle exec rake db:create:all

##8　起動
    bundle exec rails s

エラーがでなく、起動できました。
やったー。

すごく基本的なことなのに、  
はずかしながら2,3回同じエラーをみて、毎回あれれ…となったので  
メモしました。


