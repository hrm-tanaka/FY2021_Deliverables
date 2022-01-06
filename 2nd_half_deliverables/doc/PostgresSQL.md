# PostgreSQL

## 再起動

### Windows

[PostgreSQL を起動、停止する - PostgreSQL Documents - Project Group](https://www.projectgroup.info/documents/PostgreSQL/POS_000006.html)

## コマンド

### 接続

```
$ psql -h hostname -U username -d databasename
```

### 遮断

```
$ \q
```

### version

```
$postgres -V
```

### DB一覧

```
$ \l
```

### テーブル一覧

```
$ \dt
```

#### スキーマ別

```sh
$ \dt スキーマ.*
```

### テーブルの構造

```
$ \d テーブル名
```

### ユーザー一覧

```sh
$ \du
```

### DB作成

```
$ create database DB名;
```

### DB切り換え

```
$ \c DB名
```

## dump

```
$ pg_dump オプション DB名
```

### テーブル特定

```
$ pg_dump -t テーブル名 DB名
```

### オプション

* https://qiita.com/mkyz08/items/55b34f0580533907fea6
* https://www.postgresql.jp/document/9.2/html/app-pgdump.html

#### テーブルのみ

```
$ pg_dump -t テーブル名 DB名 -s
```

### 一括でdump->restore

```
$ pg_dump -Ft OLG_DB名 | pg_restore -d NEW_DB名
```

## restore

```
$ pg_restore オプション DB名
```

## restore(psql版)

```
$ psql DB名 < hoge.sql
```

```
psql -f ファイル名 -U ユーザ名 -d データベース名
```

### オプション

[pg_restore](https://www.postgresql.jp/document/9.2/html/app-pgrestore.html)

## 正規表現

* [PostgreSQLで正規表現 - Qiita](https://qiita.com/y_ito/items/a0fb46a618b0316617c8)

## スキーマ作成

### 概要

[PostgreSQLにおけるデータベース、スキーマ、テーブルの関係 | PostgreSQLの使い方](https://www.dbonline.jp/postgresql/schema/index1.html)

### 作成

[PostgreSQL 9.6.1でユーザ、データベース、スキーマ、オブジェクトを作成 | OSSでLinuxサーバ構築 | OSS Fan](http://ossfan.net/setup/postgresql-31.html)
```
$ create schema スキーマ名
```

### 一覧

```
$ \dn;
```

### 現在のDB

```
$ select current_database();
```

### セッション系関数

[その他の関数](https://www.postgresql.jp/document/7.3/user/functions-misc.html)

## Query

### select insert

[selectした結果をinsertする - Qiita](https://qiita.com/ques0942/items/acfdd5382c638580ce0b)

### あとからUnique制約追加

<https://www.compiere-distribution-lab.net/2014/12/24/postgresql-lab-%E8%A4%87%E5%90%88%E3%83%A6%E3%83%8B%E3%83%BC%E3%82%AF%E5%88%B6%E7%B4%84%E3%82%92%E4%BB%98%E5%8A%A0%E3%81%99%E3%82%8B/>

### テーブル名変更

[PostgreSQLのテーブル名を変更する　psql、pgAdmin、VBScriptでテーブル名を変更 | ＩＴ関連の技術情報サイト](http://www.cyber-funnel.com/postgres/index1323.html)

### テーブル型変更

[PostgreSQL で列データ型を変更する|Everything you do is practice](http://everything-you-do-is-practice.blogspot.com/2017/09/postgresql_26.html)

[[PostgreSQL] テーブルのカラムの変更](http://sweng.web.fc2.com/ja/database/postgresql/alter-table.html)

### truncate

```
truncate table テーブル名 restart identity;
```

### Index

[インデックスを作成する(CREATE INDEX) | PostgreSQLの使い方](https://www.dbonline.jp/postgresql/index/index1.html#section1)

## COALESCE

[PostgreSQL ISNULLやNVLのようにNULLを判定する方法](https://zukucode.com/2017/11/postgresql-coalesce.html)

## 日時フォーマット

[データ型書式設定関数](https://www.postgresql.jp/document/9.2/html/functions-formatting.html)

## 外部公開

[他ホストから接続するための設定](http://rina.jpn.ph/~rance/linux/postgresql/connect.html)

## 正規表現

* [PostgreSQLで正規表現 - Qiita](https://qiita.com/y_ito/items/a0fb46a618b0316617c8)
