ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

# Install required packages
RUN apk add --no-cache --update \
    autoconf \
    g++ \
    make \
    linux-headers \
    zlib-dev \
    libtool \
    nano

# Install and enable Xdebug
ARG XDEBUG_VERSION=latest
RUN pecl install xdebug-${XDEBUG_VERSION} && docker-php-ext-enable xdebug

# Install and enable mysql tools
RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql

# Install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN mkdir -p /var/www/html && chown www-data:www-data /var/www/html

WORKDIR /var/www/html

COPY ./www.conf /usr/local/etc/php-fpm.d/www.conf
COPY ./php.ini /usr/local/etc/php/conf.d/php.ini