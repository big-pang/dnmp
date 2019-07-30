FROM php:7.3-fpm-alpine

MAINTAINER timestrider

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories;

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
        openssl-dev

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/lib/ --with-jpeg-dir=/usr/lib/ \
    && docker-php-ext-install gd soap iconv mbstring \
    pdo pdo_mysql mysqli bz2 xml curl zip ftp opcache pdo_pgsql readline \
    && docker-php-source delete


RUN pecl install swoole && \
    pecl install redis && \
    pecl install mongodb


RUN docker-php-ext-enable swoole redis mongodb

RUN ln -snf /usr/share/zoneinfo/PRC /etc/localtime && echo PRC > /etc/TZ;


RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer


EXPOSE 9000
