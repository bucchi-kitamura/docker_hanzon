FROM php:8.1-fpm-buster 
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"] 

# コンテナ内のサーバー環境変数を設定する
ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

# apt-get update パッケージリストの更新
# apt-get -y install このコンテナで必要なパッケージをインストールする
# apt-get clean && rm -rf /var/lib/apt/lists/* 不要なキャッシュを削除する dockerで使用する容量を抑えるために実行しておくといい
# docker-php-ext-install PHPの拡張ライブラリをインストール
RUN apt-get update && \
  apt-get -y install --no-install-recommends git unzip libzip-dev libicu-dev libonig-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /data