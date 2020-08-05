# 環境構築手順

```docker-php-apache-ubuntu
├── docker-compose.yml
├── laravel
└── web
    ├── Dockerfile
    └── apache.conf
```

## Dockerfileのビルド

```console
$ docker-compose build
```

## Laravelのファイルを設置

```console
$ git clone {$Laravelのリポジトリ} laravel
```

リポジトリ（ディレクトリの名前を編集するときは）web/apache.confを編集してください
```
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/{$リポジトリ名}/public

        <Directory /var/www/html/{$リポジトリ名}/public>
            AllowOverride All
        </Directory> 
```

## Laravelの設定

```console
$ docker-compose exec web bash #コンテナ内に入る
# cd laravel
# cp .env.example .env # .envファイル生成
# composer install
```

[http://localhost/](http://localhost/)にアクセスする。

## .env設定

```
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_LOG_LEVEL=debug
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=mysql5.7
DB_PORT=3306
DB_DATABASE= #作成したDBに合わせる 
DB_USERNAME=root
DB_PASSWORD=root

BROADCAST_DRIVER=log
CACHE_DRIVER=file
SESSION_DRIVER=file
SESSION_LIFETIME=120
QUEUE_DRIVER=sync

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
```

## DB接続設定

```
$ docker-compose exec web bash #コンテナ内に入る
# cd laravel
# php artisan migrate
```

## phpMyAdminへ接続

[http://localhost:8080/](http://localhost:8080/)にアクセスで見れる
