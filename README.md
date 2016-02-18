## 現象

次のSQLを実行するとpgroongaがsegmentaion faultします。


```
SELECT
  u.url 
FROM 
  url_lists4 u
WHERE  u.url &?> Array(
  SELECT
    url 
  FROM
    keywords4
  WHERE
    name = 'esc_url'
);
```

## 検証スクリプト

* [pgroonga_like_test](https://github.com/hiroyuki-sato/pgroonga_like_test)

## 必要な環境

* vagrant 
* ansible2

## 構築する環境

* CentOS7.2
* PostgreSQL 9.5
* pgroonga: 1.0.2

## 手順

```
% vagrant up
```

```
vagrant ssh
```

/tmp/にpostgres_like_testができるので、その中にあるpgroonga_test.shを実行します。

これは単純に次のSQLを実行するだけです。

```
sudo -u postgres psql groonga_test < pgroonga_setup.sql 
sudo -u postgres psql groonga_test < create_pgroonga.sql
sudo -u postgres psql groonga_test < query_pgroonga.sql
```

```
vagrant% cd /tmp/postgres_like_test
```

```
vagrant% ./pgroonga_test.sh 
ERROR:  extension "pgroonga" does not exist
CREATE EXTENSION
NOTICE:  table "url_lists4" does not exist, skipping
DROP TABLE
CREATE TABLE
CREATE INDEX
NOTICE:  table "keywords4" does not exist, skipping
DROP TABLE
CREATE TABLE
CREATE INDEX
CREATE INDEX
COPY 500000
COPY 5000
VACUUM
VACUUM
ANALYZE
ANALYZE
Timing is on.
server closed the connection unexpectedly
	This probably means the server terminated abnormally
	before or while processing the request.
connection to server was lost
```
