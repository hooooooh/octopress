---
layout: post
title: "Gem をつくってみたい"
date: 2014-01-30 10:31:55 +0900
comments: true
categories: 
---

gem は bundlerを使って作れるみたいなので、簡単なやつをつくってみます。  


##1　Gem のテンプレート作成
    bundle gem test_libs

コマンドを実行すると、テンプレートが作られました。
    create  test_libs/Gemfile
    create  test_libs/Rakefile
    create  test_libs/LICENSE.txt
    create  test_libs/README.md
    create  test_libs/.gitignore
    create  test_libs/test_libs.gemspec
    create  test_libs/lib/test_libs.rb
    create  test_libs/lib/test_libs/version.rb


##2　作成した test_libs に移動して、Gemをインストール
    cd test_libs
    bundle install


##3　gemspec に Gem の説明
gemspec には Gem の説明や依存する他の RubyGems があればそれも書きます。    

まずは、Gem の説明は、 test_libs/test_libs.gemspec の中に  
記述箇所がわかる様に親切に TODO: があるので TODO: 部分を書きます。

    spec.summary       = %q{TODO: Write a short summary. Required.}
    spec.description   = %q{TODO: Write a longer description. Optional.}

もし、依存する RubyGems があれば追加して書きます。
    spec.add_dependency '依存するRubyGems'


##4　test_libs を読み込んでみる
    bundle exec irb
    > require 'test_libs'
    => true


##5　ライブラリとなるプログラム処理を実装
メインとなる処理自体は、 test_libs/lib/test_libs.rb に書きます。

    require "test_libs/version"
    
    module TestLibs
      # Your code goes here...
    end

また丁寧に # Your code goes here... とあるので、メソッドを追加します。  
test メソッド,test02 メソッドを追加しました。

    require "test_libs/version"
    
    module TestLibs
      def self.test
        'hello !'
      end
      
      def test02
        'hi !'
      end
    end


##6　実行してみる
    bundle exec irb
    irb(main):001:0> require 'test_libs'
    => true
    irb(main):002:0> TestLibs.methods(false)
    => [:test]
    irb(main):003:0> TestLibs.test
    => "hello !"
    irb(main):004:0> include TestLibs
    => Object
    irb(main):005:0> self.methods.include?(:test02)
    => true
    irb(main):006:0> test02
    => "hi !"
    irb(main):007:0>



##7　Gem をビルド
bundler で作ったテンプレートには gem パッケージ用のタスクが含まれているので、
それを使ってビルドします。

    bundle exec rake build
    test_libs 0.0.1 built to pkg/test_libs-0.0.1.gem.

##8　Gem をインストール
    gem install -l pkg/test_libs-0.0.1.gem -V

##9 インストールした Gem を確認
    gem list

リストに作成した Gem が表示されていればインストールされています    


作った gem は以下で公開もできるそうです。いくつあるんだろ…。  
[RubyGems.org](http://rubygems.org/gems)
















