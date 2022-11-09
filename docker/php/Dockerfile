#FROM php:8.0-apache-bullseye
FROM php:8.1-apache-bullseye

RUN apt-get update \
 && apt-get install -y zlib1g-dev libzip-dev unzip\
 && docker-php-ext-install zip
RUN cd /etc/apache2/mods-enabled \
 && ln -s ../mods-available/rewrite.load

ENV COMPOSER_ALLOW_SUPERUSER 1
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

ADD docker/php/php.ini /usr/local/etc/php/
ADD docker/php/apache/000-default.conf /etc/apache2/sites-enabled/

WORKDIR /var/www/html

COPY ../../../project /var/www/html
COPY ../../../docker/php/apache/000-default.conf /etc/apache2/sites-available/000-default.conf