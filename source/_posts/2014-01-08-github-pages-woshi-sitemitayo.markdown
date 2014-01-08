---
layout: post
title: "GitHub Pages を試してみたよ"
date: 2014-01-08 21:57:40 +0900
comments: true
categories: 
---
GitHub Pagesを試してみました。

以下の記事を参考にしました。

[http://morizyun.github.io/blog/octopress-gitpage-minimum-install-guide/](http://morizyun.github.io/blog/octopress-gitpage-minimum-install-guide/)
[http://randd.kwappa.net/2013/04/16/521](http://randd.kwappa.net/2013/04/16/521)

ほとんど参考記事のまねっこだけど、私が試したことをメモメモ…。


###1　GitHub にリポジトリを作成

リポジトリ名は [username].github.io にします。  
[username]には自分のユーザ名を入れます。  
私の場合は、ユーザー名が hooooooh なので、「hooooooh.github.io」で作成しました。  

###2　Octopress をセットアップ

Octopress は jekyll を使って作るブログ構築用のフレームワークで、  
GitHub Pages と組み合わせると、とても簡単にブログが作れる。
しかも無料！

セットアップは公式サイトにのっています。  
[http://octopress.org/docs/setup/](http://octopress.org/docs/setup/)

    git clone git@github.com:imathis/octopress.git [username].github.io
    cd username.github.io
    gem install bundler
    bundle install
    bundle exec rake install
    bundle exec rake setup_github_pages

デプロイ先を聞かれるので、  
    git@github.com:[username]/[username].github.com.git
と入力。

できたー。

###3　_config.yml に設定項目を記入
公式サイトの_config.yml設定の部分を見ながら必要なところだけ記入  
[http://octopress.org/docs/configuring/](http://octopress.org/docs/configuring/)

    url: http://[username].github.io
    title: hoge → サイトのタイトルをいれます
    subtitle: fuga → サイトのサブタイトルをいれます
    author: 09mura
    simple_search: http://google.com/search
    description:

###4　記事を作成する
記事のタイトルをきめて以下を実行します。
    bundle exec rake new_post['記事のタイトル']

そうすると、source/_post/YYYY-MM-DD-title.markdownが作られるので  
あとは、Markdownやhtmlで記事を書きます。

###5　ローカルで確認
以下を実行してブラウザで http://localhost:4000/ にアクセスしたらローカルで確認できます。
    bundle exec rake preview

###6　テーマを変える
テーマいろいろあるけど…  
[http://opthemes.com/](http://opthemes.com/)  
わたしは darkStripes というテーマにしてみました。  
以下を実行してテーマを適用します。

    git clone https://github.com/amelandri/darkstripes.git .themes/darkstripes
    bundle exec rake install['darkstripes']

###7　GitPageへデプロイする
以下を実行してデプロイします。
    bundle exec rake deploy

まだまだわからないことばかりだけど…  
ソースコードもGitHubで管理できるので、便利そうです。

画像もなくさみしい記事になちゃったな...。  
少しづつよくしていきたい。


