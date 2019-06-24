# 2019年 Webプログラミング演習Ⅲ&Ⅳ

- 更新: 2019/05/28

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
    $ cd
    $ cd webpro
    $ docker-compose up -d
    ```
5. ブラウザで[http://localhost:8080/](http://localhost:8080/)にアクセスし起動を確認する。(Docker Toolbox で Docker をインストールしている場合は、[http://192.168.99.100:8080](http://192.168.99.100:8080)にアクセスする)

#### 演習環境を停止する

```console
$ docker-compose down
```


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

### サンプルコード

- [work.zip](https://hamasyou-dhw.github.io/webpro/201904/work.zip)

## 5/28(火) 演習

データベースを利用します。データベースは演習環境に組み込まれている MySQL を使用します。

### 起動方法

演習環境の構築方法に従って、演習環境を起動しておいてください。
起動したら、サーバにログインします。

```console
$ docker container ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                NAMES
8d0a506d2706        webpro_app          "docker-php-entrypoi…"   10 seconds ago      Up 9 seconds        0.0.0.0:8080->80/tcp                 webpro_app_1
eeb1a9e328e1        mysql:5.7           "docker-entrypoint.s…"   11 seconds ago      Up 10 seconds       33060/tcp, 0.0.0.0:43306->3306/tcp   webpro_db_1

$ docker container exec -it 8d0a506d2706 bash
root@8d0a506d2706:/var/www/html# mysql -u root -h db
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.25 MySQL Community Server (GPL)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]>
```

これで MySQL に接続できます。

## データベースを作成する

```console
MySQL [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.02 sec)

MySQL [(none)]> create database webprodb default charset utf8;
Query OK, 1 row affected (0.01 sec)

MySQL [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| webprodb           |
+--------------------+
5 rows in set (0.02 sec)

MySQL [(none)]> use webprodb;
Database changed
```

## テーブルを作成する

```console
MySQL [webprodb]> show tables;
Empty set (0.01 sec)

MySQL [webprodb]> create table students (code CHAR(8) NOT NULL, name VARCHAR(255) NOT NULL, grade INT NOT NULL);
Query OK, 0 rows affected (0.03 sec)

MySQL [webprodb]> show tables;
+--------------------+
| Tables_in_webprodb |
+--------------------+
| students           |
+--------------------+
1 row in set (0.01 sec)
```

## データを挿入する

```console
MySQL [webprodb]> insert into students (code, name, grade) values ("A01DC001", "Syougo Hamada", 3);
```

## データを表示する（選択する）

```console
MySQL [webprodb]> select * from students;
+----------+---------------+-------+
| code     | name          | grade |
+----------+---------------+-------+
| A01DC001 | Syougo Hamada |     3 |
+----------+---------------+-------+
1 row in set (0.00 sec)
```

## データを更新する

```console
MySQL [webprodb]> update students set name = "Shogo Hamada" where code = "A01DC001";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MySQL [webprodb]> select * from students;
+----------+--------------+-------+
| code     | name         | grade |
+----------+--------------+-------+
| A01DC001 | Shogo Hamada |     3 |
+----------+--------------+-------+
1 row in set (0.00 sec)
```

## データを削除する

```console
MySQL [webprodb]> delete from students where code = "A01DC001";
Query OK, 1 row affected (0.00 sec)

MySQL [webprodb]> select * from students;
Empty set (0.00 sec)
```

## 2019/06/24

- [frontend.zip](frontend.zip)

```console
unzip frontend.zip
docker-compose build
docker-compose up -d
```

[http://localhost:8080/test](http://localhost:8080/test)