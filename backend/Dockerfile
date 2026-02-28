FROM php:8.3-fpm-alpine

# ビルド用依存パッケージ
RUN apk add --no-cache --virtual .build-deps \
  $PHPIZE_DEPS \
  postgresql-dev

# 実行時に必要なライブラリ
RUN apk add --no-cache postgresql-libs

# pgsql拡張インストール
RUN docker-php-ext-install pdo_pgsql

# ビルド依存削除（軽量化）
RUN apk del .build-deps

COPY --from=composer:2.9.2 /usr/bin/composer /usr/bin/composer
COPY php.ini /usr/local/etc/php/conf.d/99-etc.ini

ADD docker-entrypoint.sh ./
RUN chmod +x ./docker-entrypoint.sh

WORKDIR /var/www/laravel

CMD ["./docker-entrypoint.sh"]
