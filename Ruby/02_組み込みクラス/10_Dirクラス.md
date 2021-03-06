10 Dirクラス
===========

## 目次

* [Dirクラスとは](#0Dirクラスとは)

* [ディレクトリを開閉する](#1ディレクトリを開閉する)

* [開いているディレクトリのパスの取得](#2開いているディレクトリのパスの取得)

* [カレントディレクトリの取得](#3カレントディレクトリの取得)

* [カレントディレクトリの移動](#4カレントディレクトリの移動)

* [ディレクトリの作成](#5ディレクトリの作成)

* [ディレクトリの削除](#6ディレクトリの削除)


## 0.Dirクラスとは

ディレクトリの移動や作成、ディレクトリ内のファイル一覧の取得など、ディレクトリを扱うクラス



## 1.ディレクトリを開閉する

* `open`メソッド：ディレクトリを開く

  * 返り値は`Dir`クラスのオブジェクト

  * 例えば`each`メソッドでファイル一覧を取得できる

* `close`メソッド：開いたディレクトリを閉じる

```ruby
>> dir = Dir.open("/usr/local/bin")
=> #<Dir:/usr/local/bin>
>> dir.each{|file| puts file}
.
..
pg_standby
pg_rewind
# ・・・(省略)・・・
convert
pg_dump
pydoc2
=> #<Dir:/usr/local/bin>
>> dir.close
=> nil
```



## 2.開いているディレクトリのパスの取得

* `path`メソッド：開いているディレクトリのパスを取得

* `Dir.open`メソッドはブロックを取ることができ、この場合はブロックを出るときに自動的に閉じられる

```ruby
>> Dir.open("/usr/local/bin"){|dir| puts dir.path}
/usr/local/bin
=> nil          # 自動的に閉じられる
```



## 3.カレントディレクトリの取得

* `Dir.pwd`、`Dir.getwd`メソッド：カレントディレクトリを取得する

```ruby
>> Dir.pwd
=> "/Users/MacUser/work/rails/shared_hobby"
```



## 4.カレントディレクトリの移動

* `Dir.chdir`メソッド：カレントディレクトリを指定されたディレクトリに変更する。

* 指定がない場合、環境変数 **HOME** や **LOGDIR** が設定されていれば、そのディレクトリに移動する

* ブロックが与えられた場合には、そのブロック内でのみディレクトリを移動し、ブロックを出るときに元に戻る

* ディレクトリの移動に成功すれば0を返す

```ruby
>> Dir.chdir("/usr/local")
=> 0
>> Dir.pwd
=> "/usr/local"
>> Dir.chdir("/usr/local/bin"){|dir| puts Dir.pwd}
/usr/local/bin
=> nil
>> Dir.pwd
=> "/usr/local"
```



## 5.ディレクトリの作成

* `mkdir`メソッド：指定したパスのディレクトリを作成する

* 2つ目の引数にパーミッション(mode)を指定可能

* 通常、パーミッションは3桁の8進数で指定

* 実際のパーミッションは、指定された値と`unmask`をかけた値(`mode & ~unmask`)となる

```ruby
>> Dir.mkdir("/tmp/foo")
=> 0
>> Dir.mkdir("/tmp/bar", 0755)
=> 0
```



## 6.ディレクトリの削除

* `rmdir`メソッド：ディレクトリを削除する

```ruby
>> Dir.mkdir("/tmp/foo")
=> 0
>> Dir.rmdir("/tmp/foo")
=> 0
```



| 版     | 年/月/日   |
| ------ | ---------- |
| 第二版 | 2019/05/11 | 
