# README

Rails7 +　 MySQL 環境

### 環境構築

### 必要ファイル

- Dockerfile
- docker-compose.yml
- Gemfile
- Gemfile.lock
- entrypoint.sh

#### Rails プロジェクトの作成

```
docker-compose run web rails new . --force --no-deps --database=mysql
```

- docker-compose run 引数で指定したコンテナ内でコマンドを実行する
- database=mysql で DB 設定を MySQL にした状態でプロジェクト作成。

#### DB 接続設定(database.yml)

```
development:
  <<: *default
  database: myapp_development
  host: db
  username: root
  password: password

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  <<: *default
  database: myapp_test
  host: db
  username: root
  password: password
```

#### DB 作成

```
docker-compose run web db:migrate:reset
```

#### Docker イメージ起動

```
docker-compose up -d
```

http://localhost:3000/ にアクセスしてページが表示されたら成功。
