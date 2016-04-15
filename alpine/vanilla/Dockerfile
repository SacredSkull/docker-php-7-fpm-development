FROM php:7-fpm-alpine
	
RUN apk add --update zlib unzip git && rm -rf /var/cache/apk/*

RUN docker-php-ext-install pdo pdo_mysql zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www
