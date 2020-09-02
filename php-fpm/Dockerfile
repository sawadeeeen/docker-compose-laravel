FROM php:7.4.4-fpm

# GitとPHP拡張のインストール
RUN set -eux \
 && apt-get update && apt-get install -y git autoconf g++ libtool make libzip-dev libpng-dev libjpeg-dev libfreetype6-dev unzip \
 && docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-freetype=/usr/include/ \
 && docker-php-ext-configure opcache --enable-opcache \
 && docker-php-ext-install opcache bcmath pdo_mysql gd exif zip  \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists

# install composer
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN set -eux \
 && composer global require hirak/prestissimo

WORKDIR /var/www/laravel

