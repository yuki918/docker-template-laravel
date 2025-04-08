# ベースイメージの指定
FROM php:8.2-fpm

# 作成した設定ファイルをコンテナ内にコピー
COPY php.ini /usr/local/etc/php/php.ini

# パッケージのインストール
RUN apt-get update \
    && apt-get -y install git zip unzip vim

RUN docker-php-ext-install pdo_mysql

# composerのインストール（https://hub.docker.com/_/composer）
COPY --from=composer /usr/bin/composer /usr/bin/composer

# コンテナ内で作業する際のカレントディレクトリの指定
WORKDIR /var/www/html