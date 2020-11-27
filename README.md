
# 日本の祝日判定Rubyプログラム

([GitHub](https://github.com/masa16/holiday_japan)),
([RubyGems](https://rubygems.org/gems/holiday_japan))

## 特徴
* 1948年7月20日以降の日本の国民の祝日、振替休日、および国民の休日を計算して判定。
* スクリプトコード([holiday_japan.rb](https://github.com/masa16/holiday_japan/blob/master/lib/holiday_japan.rb))は、祝日データを含めて200行弱とコンパクト。

(date2 の holiday.rb と比較して)
* 祝日をキャッシュすることにより、大量の日付について祝日判定する場合でも高速に動作
* 祝日名を返すことが可能
* 祝日のルールをテーブルで持つことにより、法改正による祝日変更への対応が容易

([holiday_jp](https://rubygems.org/gems/holiday_jp) と比較して)
* holiday_jp は日付をキーとする祝日データセットに基く。holiday_japan は祝日ルールに基き、照会された年ごとにデータセットを生成する。

## インストール

* RubyGems によるインストール
  ```
  gem install holiday_japan
  ```

* または、[holiday_japan.rb](https://github.com/masa16/holiday_japan/blob/master/lib/holiday_japan.rb)
  のスクリプトファイルを ruby のライブラリパスに置く

## 使い方

### モジュールをロード

  ```ruby
  require 'holiday_japan'
  ```

### HolidayJapan モジュール関数

* `check(date)` ― Dateクラスのオブジェクトによる祝日判定

  ```ruby
  HolidayJapan.check(Date.new(2021,3,20))
  => true
  ```


* `name(date)` ― 日付が祝日の場合は祝日名を返し、祝日でなければ nil を返す。

  ```ruby
  HolidayJapan.name(Date.new(2021,3,20))
  => "春分の日"
  ```


* `print_year(year)` ― ある年の祝日一覧をプリント

  ```
  $ ruby -r holiday_japan -e 'HolidayJapan.print_year 2021'
  listing year 2021...
  2021-01-01 Fri 元日
  2021-01-11 Mon 成人の日
  2021-02-11 Thu 建国記念の日
  2021-02-23 Tue 天皇誕生日
  2021-03-20 Sat 春分の日
  2021-04-29 Thu 昭和の日
  2021-05-03 Mon 憲法記念日
  2021-05-04 Tue みどりの日
  2021-05-05 Wed こどもの日
  2021-07-22 Thu 海の日
  2021-07-23 Fri スポーツの日
  2021-08-08 Sun 山の日
  2021-08-09 Mon 振替休日
  2021-09-20 Mon 敬老の日
  2021-09-23 Thu 秋分の日
  2021-11-03 Wed 文化の日
  2021-11-23 Tue 勤労感謝の日

  ```

* `list_year(year)` ― ある年について、 [日付, 祝日名] のArrayを返す

  ```ruby
  HolidayJapan.list_year(2021)
  => [[#<Date: 2021-01-01 ((2459216j,0s,0n),+0s,2299161j)>, "元日"],
      [#<Date: 2021-01-11 ((2459226j,0s,0n),+0s,2299161j)>, "成人の日"],
      [#<Date: 2021-02-11 ((2459257j,0s,0n),+0s,2299161j)>, "建国記念の日"],
      [#<Date: 2021-02-23 ((2459269j,0s,0n),+0s,2299161j)>, "天皇誕生日"],
      [#<Date: 2021-03-20 ((2459294j,0s,0n),+0s,2299161j)>, "春分の日"],
      [#<Date: 2021-04-29 ((2459334j,0s,0n),+0s,2299161j)>, "昭和の日"],
      [#<Date: 2021-05-03 ((2459338j,0s,0n),+0s,2299161j)>, "憲法記念日"],
      [#<Date: 2021-05-04 ((2459339j,0s,0n),+0s,2299161j)>, "みどりの日"],
      [#<Date: 2021-05-05 ((2459340j,0s,0n),+0s,2299161j)>, "こどもの日"],
      [#<Date: 2021-07-22 ((2459418j,0s,0n),+0s,2299161j)>, "海の日"],
      [#<Date: 2021-07-23 ((2459419j,0s,0n),+0s,2299161j)>, "スポーツの日"],
      [#<Date: 2021-08-08 ((2459435j,0s,0n),+0s,2299161j)>, "山の日"],
      [#<Date: 2021-08-09 ((2459436j,0s,0n),+0s,2299161j)>, "振替休日"],
      [#<Date: 2021-09-20 ((2459478j,0s,0n),+0s,2299161j)>, "敬老の日"],
      [#<Date: 2021-09-23 ((2459481j,0s,0n),+0s,2299161j)>, "秋分の日"],
      [#<Date: 2021-11-03 ((2459522j,0s,0n),+0s,2299161j)>, "文化の日"],
      [#<Date: 2021-11-23 ((2459542j,0s,0n),+0s,2299161j)>, "勤労感謝の日"]]
  ```


* `hash_year(year)` ― ある年について、 {日付=>祝日名} のHashを返す

  ```ruby
  HolidayJapan.hash_year(2021)
  => {#<Date: 2021-01-01 ((2459216j,0s,0n),+0s,2299161j)>=>"元日",
      #<Date: 2021-01-11 ((2459226j,0s,0n),+0s,2299161j)>=>"成人の日",
      #<Date: 2021-02-11 ((2459257j,0s,0n),+0s,2299161j)>=>"建国記念の日",
      #<Date: 2021-02-23 ((2459269j,0s,0n),+0s,2299161j)>=>"天皇誕生日",
      #<Date: 2021-03-20 ((2459294j,0s,0n),+0s,2299161j)>=>"春分の日",
      #<Date: 2021-04-29 ((2459334j,0s,0n),+0s,2299161j)>=>"昭和の日",
      #<Date: 2021-05-03 ((2459338j,0s,0n),+0s,2299161j)>=>"憲法記念日",
      #<Date: 2021-05-04 ((2459339j,0s,0n),+0s,2299161j)>=>"みどりの日",
      #<Date: 2021-05-05 ((2459340j,0s,0n),+0s,2299161j)>=>"こどもの日",
      #<Date: 2021-07-22 ((2459418j,0s,0n),+0s,2299161j)>=>"海の日",
      #<Date: 2021-07-23 ((2459419j,0s,0n),+0s,2299161j)>=>"スポーツの日",
      #<Date: 2021-08-08 ((2459435j,0s,0n),+0s,2299161j)>=>"山の日",
      #<Date: 2021-08-09 ((2459436j,0s,0n),+0s,2299161j)>=>"振替休日",
      #<Date: 2021-09-20 ((2459478j,0s,0n),+0s,2299161j)>=>"敬老の日",
      #<Date: 2021-09-23 ((2459481j,0s,0n),+0s,2299161j)>=>"秋分の日",
      #<Date: 2021-11-03 ((2459522j,0s,0n),+0s,2299161j)>=>"文化の日",
      #<Date: 2021-11-23 ((2459542j,0s,0n),+0s,2299161j)>=>"勤労感謝の日"}
  ```


* `between(from_date,to_date)` ― from_date から to_date までの祝日について、{日付=>祝日名}のHashを返す

  ```ruby
  HolidayJapan.between("2021-4-1","2022-3-31")
  => {#<Date: 2021-04-29 ((2459334j,0s,0n),+0s,2299161j)>=>"昭和の日",
      #<Date: 2021-05-03 ((2459338j,0s,0n),+0s,2299161j)>=>"憲法記念日",
      #<Date: 2021-05-04 ((2459339j,0s,0n),+0s,2299161j)>=>"みどりの日",
      #<Date: 2021-05-05 ((2459340j,0s,0n),+0s,2299161j)>=>"こどもの日",
      #<Date: 2021-07-22 ((2459418j,0s,0n),+0s,2299161j)>=>"海の日",
      #<Date: 2021-07-23 ((2459419j,0s,0n),+0s,2299161j)>=>"スポーツの日",
      #<Date: 2021-08-08 ((2459435j,0s,0n),+0s,2299161j)>=>"山の日",
      #<Date: 2021-08-09 ((2459436j,0s,0n),+0s,2299161j)>=>"振替休日",
      #<Date: 2021-09-20 ((2459478j,0s,0n),+0s,2299161j)>=>"敬老の日",
      #<Date: 2021-09-23 ((2459481j,0s,0n),+0s,2299161j)>=>"秋分の日",
      #<Date: 2021-11-03 ((2459522j,0s,0n),+0s,2299161j)>=>"文化の日",
      #<Date: 2021-11-23 ((2459542j,0s,0n),+0s,2299161j)>=>"勤労感謝の日",
      #<Date: 2022-01-01 ((2459581j,0s,0n),+0s,2299161j)>=>"元日",
      #<Date: 2022-01-10 ((2459590j,0s,0n),+0s,2299161j)>=>"成人の日",
      #<Date: 2022-02-11 ((2459622j,0s,0n),+0s,2299161j)>=>"建国記念の日",
      #<Date: 2022-02-23 ((2459634j,0s,0n),+0s,2299161j)>=>"天皇誕生日",
      #<Date: 2022-03-21 ((2459660j,0s,0n),+0s,2299161j)>=>"春分の日"}
  ```


### 祝日データをCSVに出力

  ```
  $ ruby -r csv -r holiday_japan -e 'CSV.open("holiday.csv","w"){|c| HolidayJapan.between(2020,2021).each{|a| c<<a}}'

  $ head -n3 holiday.csv ; echo ...; tail -n3 holiday.csv
  2020-01-01,元日
  2020-01-13,成人の日
  2020-02-11,建国記念の日
  ...
  2021-09-23,秋分の日
  2021-11-03,文化の日
  2021-11-23,勤労感謝の日

  ```

## 祝日データ

* 1948年7月20日(祝日法発令) 以降の祝日に対応
* 2021年の[暦要項](http://eco.mtk.nao.ac.jp/koyomi/yoko/)まで確認（法改正がない限り以降も有効）
* 春分の日・秋分の日の計算は2150年まで

## Author:
    Masahiro TANAKA

## Copyright:
    (C) Copyright 2003-2020 by Masahiro TANAKA
    This program is free software under MIT license.
    See LICENSE.txt.
    NO WARRANTY.

## Version:
    2018-04-14  ver 1.4  祝日データ仕様変更、2019,2020年対応
    2017-12-01  ver 1.3  print_between 関数追加
    2015-04-11  ver 1.2  hash_year, between 関数追加
    2014-05-23  ver 1.1  「山の日」追加
    2012-12-23  ver 1.0  モジュール名を Holiday から HolidayJapan に変更
    2007-08-02  ver 0.9  リファクタリング
    2007-03-08  ver 0.8  祝日データクラスを統一、データを配列で記述
    2006-02-06  ver 0.7  平成19年(西暦2007年)の暦要項 反映(祝日法改正)
                         Holiday.create_table 修正
                         Holiday.list_year 追加
    2003-10-02  ver 0.6  祝日データ追加
    2003-09-29  ver 0.5
    2003-09-22  ver 0.4
    2003-09-20  ver 0.3
    2003-09-16  ver 0.2
    2003-09-15  ver 0.1
