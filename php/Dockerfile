FROM php:7.3-fpm-alpine

MAINTAINER timestrider

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories;

RUN apk update && apk add --no-cache \
        freetype-dev \
        jpeg-dev \
        libjpeg-turbo-dev \
        libxml2-dev \
        postgresql-dev \
        libressl-dev \
        bzip2-dev \
        libzip-dev \
        libedit-dev \
        tzdata  \
        curl-dev \
        $PHPIZE_DEPS \
        openssl-dev \
        imagemagick-dev

RUN docker-php-ext-configure  gd  --with-freetype-dir=/usr/lib/ --with-jpeg-dir=/usr/lib/
RUN docker-php-ext-install gd soap iconv mbstring \
    pdo pdo_mysql mysqli bz2 xml curl zip  opcache pdo_pgsql readline
RUN docker-php-source delete


RUN pecl install swoole
RUN pecl install redis
RUN pecl install mongodb
RUN pecl install imagick


RUN docker-php-ext-enable swoole redis mongodb imagick

#RUN ln -snf /usr/share/zoneinfo/PRC /etc/localtime && echo PRC > /etc/TZ;


RUN php -r "copy('https://getcomposer.org/download/1.8.6/composer.phar', '/usr/local/bin/composer');" \
    && chmod +x /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
#RUN php composer-setup.php
#RUN php -r "unlink('composer-setup.php');"
#RUN mv composer.phar /usr/local/bin/composer
