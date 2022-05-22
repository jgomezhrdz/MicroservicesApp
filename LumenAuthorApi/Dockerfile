FROM php:7.4-fpm-alpine

WORKDIR /var/www/html/

RUN apk update

RUN apk add --no-cache bash curl \
    php7 \
    php7-fpm \ 
    php7-zip \
    php7-pdo \
    php7-pdo_mysql \
    php7-openssl \
    php7-zlib \
    zip libzip-dev icu-dev libxml2-dev

RUN docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install zip xml \
    && docker-php-ext-install pdo_mysql

RUN curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer

COPY ./composer.json ./composer.lock ./
COPY ./tests ./tests
COPY ./database ./database

RUN composer update

COPY . .

CMD php -S 0.0.0.0:80 -t public