# 2019年 Webプログラミング演習Ⅲ&Ⅳ

## 演習環境

本講義では、演習環境を [Docker](https://www.docker.com/) で構築する。
Windows 環境では、[Docker Desktop for Windows](https://docs.docker.com/install/#desktop)、Mac 環境では [Docker Desktop for Mac](https://docs.docker.com/install/#desktop) をそれぞれインストールする。

Windows 環境で、OS エディションにより Docker をインストールできない場合は、[Docker Toolbox](https://docs.docker.com/toolbox/overview/) を利用し、Virtual Box 上に Docker をインストールする。

1. Docker をインストールする
2. ホームディレクトリに、*webpro* ディレクトリを作成する
3. webpro ディレクトリに、次の2つのファイルをダウンロードする
    - [Dockerfile](https://hamasyou-dhw.github.io/webpro/201904/Dockerfile)
    - [docker-compose.yml](https://hamasyou-dhw.github.io/webpro/201904/docker-compose.yml)
4. 次のコマンドを入力し、演習環境を起動する

    ```console
    $ cd webpro
    $ docker-compose up
    ```
5. ブラウザで[http://localhost:8080/](http://localhost:8080/)にアクセスし起動を確認する。(Docker Toolbox で Docker をインストールしている場合は、[http://192.168.99.100:8080](http://192.168.99.100:8080)にアクセスする)



## 5/7(火) 演習

ECサイトを作りながら、順次、設計を更新していく演習を行う。

1. ECサイトを作成する
2. MVC アーキテクチャで作り直す
3. データベースをつかってみる

### ECサイトを作成する

まずは、既存の知識で ECサイトを作ってみます。
次の機能をもつWebアプリケーションを作成しましょう。

- 商品登録機能
    - 商品を登録できる画面
- 商品一覧機能
    - 登録していある商品を一覧表示する画面
    - 商品を選択して、カートに登録する機能
    - カートへの登録は、セッションを利用する
- カート
    - 登録されている商品と合計金額を表示する画面

商品情報は次の通り

- 商品名
- 商品コード
- 商品画像
- 本体価格 (税抜円)
- 色 (赤/青/白/黒)
- サイズ (S/M/L)

