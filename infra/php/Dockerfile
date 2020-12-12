FROM php:8.0-rc-fpm-buster
# https://hub.docker.com/_/php

# パイプ中のあらゆる段階でエラーがあれば失敗とする
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

# 構築時点では2.0.8がインストールされた
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

# 1. インストール可能なパッケージ一覧を更新。インストールやアップグレードは行わない
# 2. Laravelのインストールに必要なパッケージをインストール
# 3. 2で使用したキャッシュファイルを削除
RUN apt-get update && \
  apt-get -y install git unzip libzip-dev libicu-dev libonig-dev libpng-dev && \
  docker-php-ext-install -j$(nproc) pdo_mysql gd && \
  apt-get clean && rm -rf /var/lib/apt/lists/*

COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /work