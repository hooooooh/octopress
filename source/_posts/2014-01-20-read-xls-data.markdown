---
layout: post
title: "Excel のデータを読み込んで JSON にしたいよ"
date: 2014-01-20 23:21:26 +0900
comments: true
categories: 
---
Excel のデータを読み込んで JSON にする処理があったので、  
スプレッドシートをパース出来る roo という gem を使ってみました。    

[roo のGitHubページ](https://github.com/Empact/roo)  
[roo の公式サイト](http://roo.rubyforge.org/)


##1　Gemfile に gem roo を追加
    gem 'roo'

##2　Excel を読み込んで JSON にする処理

こんな xlsx を読み込みたい  
![](../images/2014-01-20-read-xls-data/xls_img_01.png =245x202)

    def roo_test
        
        # Excelデータを取得する
        xls = Roo::Spreadsheet.open('Excelへのパス')

        # JSON データを入れる用
        data_list = []

        xls.each_with_pagename do |name, sheet|
            if name == '読み込みたいシート名'

                row_count = sheet.last_row.to_i

                column_name_ary = sheet.row(1)

                (2..row_count).each do |index|
                    xls_row_data = sheet.row(index)
                    row_data = {}
                    row_data[column_name_ary[0]] = xls_row_data[0]
                    row_data[column_name_ary[1]] = xls_row_data[1]
                    data_list.push(row_data)
                end
            end
        end
        render json: data_list
    end

##3　JSONできました
[{"name":"aaa","mail_address":"bbb@ccc.com"},{"name":"hoge","mail_address":"fuga@piyo.com"}]    