FROM php:7-fpm-alpine

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug
	
RUN apk add --update zlib zlib-dev unzip git && rm -rf /var/cache/apk/*

RUN docker-php-ext-install pdo pdo_mysql zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www
