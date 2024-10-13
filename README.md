# My Project
laravel-app deployment
====

Overview

### docker images
- laravel-nginx
  - nginx:1.25.3-alpine3.18
- laravel-app
  - php:8.2-fpm-alpine
- laravel-db
  - mysql:8.0.39-debian
- laravel-redis
  - redis:latest(v=7.4.0)

## ローカルPCのhosts設定
- /etc/hosts
```
127.0.0.1 dev-laravel.menta.work
```

## 参考ドキュメント
- https://laravel.com/docs/11.x
- https://laravel.com/docs/11.x/deployment#nginx
- https://laravel.com/docs/11.x/redis

### voleme  mount設定
laravel-nginxとlaravel-appでphp-fpm.sockファイル共有出来るようにphp-fpm-sock:volumesを作成　\
コンテナ削除後もlaravelapp設定が残るように~/git/github/menta/dev_laravel:/var/www:にマウント 


### docker起動

```
docker-compose up -d --build
docker ps -a
```

### Laravel appダウンロード
```
docker exec -it laravel-app bash
composer create-project --prefer-dist laravel/laravel app
cd app
php artisan -v
composer install
composer -v
php artisan key:generate
php artisan config:cache
vim .env #MYSQLとRedis接続するための環境変数を定義
php artisan migrate
```

### アクセス
http://dev-laravel.menta.work/

