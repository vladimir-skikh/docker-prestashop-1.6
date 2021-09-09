ARG PHP_VERSION=5.6

FROM php:${PHP_VERSION}-fpm

RUN apt-get update && apt-get install -y \
        curl \
        wget \
        git \
        libfreetype6-dev \
        libonig-dev \
        libpq-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libzip-dev \
        libicu-dev \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure iconv \
    && docker-php-ext-configure mbstring \
    && docker-php-ext-configure mysqli \
    && docker-php-ext-configure pdo_mysql \
    && docker-php-ext-configure zip \
    && docker-php-ext-configure fileinfo \
    && docker-php-ext-install -j$(nproc) mcrypt iconv mbstring mysqli pdo_mysql zip fileinfo intl gd \
    && docker-php-ext-enable mcrypt \
    && docker-php-ext-enable iconv \
    && docker-php-ext-enable mbstring \
    && docker-php-ext-enable mysqli \
    && docker-php-ext-enable pdo_mysql \
    && docker-php-ext-enable zip \
    && docker-php-ext-enable fileinfo \
    && docker-php-ext-enable intl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD php.ini /usr/local/etc/php/conf.d/php.ini

WORKDIR /var/www

CMD ["php-fpm"]