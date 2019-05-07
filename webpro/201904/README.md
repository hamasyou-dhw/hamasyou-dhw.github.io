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
    ```
    $ cd webpro
    $ docker-compose up
    ```
5. ブラウザで[http://localhost:8080/](http://localhost:8080/)にアクセスし起動を確認する。(Docker Toolbox で Docker をインストールしている場合は、[http://192.168.99.100:8080](http://192.168.99.100:8080)にアクセスする)


