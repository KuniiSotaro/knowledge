07 diffコマンド
==============

* `diff`コマンド：2つのファイルを差分を表示するコマンド

  ```bash
  diff [オプション]<比較元ファイル> <比較先ファイル>
  ```

  * このコマンドは、設定ファイルやプログラムのコードに対して、**編集前と編集後の変更内容を確認するためによく使われる**

  * 例)`.bashrc`とコピーした`.bashrc.org`の、`PS1`の値を編集した場合

  ```bash
  $ diff .bashrc.org .bashrc
  2c2
  < PS1='\$ '
  ---
  > PS1='[\u@\h] \w\$ '
  ```

  * 最初の「2c2」は、元ファイルからどの行をどのように変更したのかを示している

    * この部分は「変更コマンド」と呼ばれ、「<変更範囲1><変更種別><変更範囲2>」という形式

    * 変更種別は`a`、`c`、`d`の3種類がある

    * それぞれ、Addの`a`、Changeの`c`、Deleteの`d`として表されている

| 記号            | 内容                                                                     |
| --------------- | ------------------------------------------------------------------------ |
| <範囲1>a<範囲2> | 1つ目のファイルの範囲1の後に、2つ目のファイルの範囲2の内容が追加された   |
| <範囲1>c<範囲2> | 1つ目のファイルの範囲1の箇所が、2つ目のファイルの範囲2の内容に変更された |
| <範囲1>d<範囲2> | 1つ目のファイルの範囲1の箇所が削除された                                 |

    * つまり、「`.bashrc.org`ファイルの12行目が`.bashrc`ファイルの12行目に変更された」ということを意味している

  ![diffの変更種別](./images/diffの変更種別.png)

  * `diff`コマンドの出力の2行目以降は、ファイルの実際の変更内容を表示している

  * 行の先頭にある`<`は、1つ目のファイルにだけある行を表す

  * `>`は2つ目のファイルにだけある行を表している

    * つまり、1つ目のファイルから2つ目のファイルへと変更する際に、`<`は削除された行、`>`は追加された行という意味になる

    ```bash
    # 削除された行
    < PS1='\$ '
    ---
    # 追加された行
    > PS1='[\u@\h] \w\$ '
    ```

* この際には変更のあった行のみが表示されるので、2つのコマンドで共通する列は表示されない

* ファイル内で複数の行を変更した場合には、それぞれの箇所が差分として表示される



## ユニファイド出力形式

* `ユニファイド形式`：`diff`コマンドに`-u`オプションをつけることで出力できる

  * 最初の2行に指定した2つのファイルのファイル名と更新日時が表示される

  * 3行目から差分の表示で、追加された行は先頭に`+`が、削除された行には先頭に`-`が表示される

  * 変更のあった行だけでなくそれらの前後何行かも含めて表示される

  * `@@`で始まる行は、その差分が元のファイルの何行目に対応しているかを示す

    ```bash
    @@ -<1つ目のファイルの変更開始行>,<変更行数> +<2つ目のファイルの変更開始行>,<変更行数> @@
    ```



## 差分の使い方とパッチ

* `パッチ`：修正内容を共有する目的で使用する差分ファイル

  * `diff`コマンドで出力された差分は、`patch`コマンドでパッチを当てる(修正を適用する)

  * パッチを当てる際、ユニファイド出力形式にするとエラーが発生しにくい



| 版   | 年/月/日   |
| ---- | ---------- |
| 初版 | 2019/04/08 |
