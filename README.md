# laravel-book-sample-1

# 実行環境に関して

参考: 
- [インストール](https://zenn.dev/nagi125/articles/ea1d314c94409341a3b0)
- [インストール後の各種設定](https://qiita.com/schrosis/items/cce304870fcb27498a5e)

```
docker-compose up -d

# 初期設定時
docker-compose exec app bash -c 'cd ./app $$ composer create-project --prefer-dist laravel/laravel . "8.*"'

# app配下が作成されている場合
docker-compose exec app bash -c "cd ./app && composer install"

# db migrate
docker-compose exec app php artisan migrate
```


# db内の確認

```
docker-compose exec db bash
psql -U postgres
\l

# データベース接続
\c laravel-db

# テーブル一覧
\dt
```

# ローカルdbの削除

```
docker-compose down
docker volume rm laravel-book-sample-1_db
```

# コマンド

```
php artisan test:make
php artisan test tests/Feature/HomeTest.php
```