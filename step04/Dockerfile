FROM php:7.1-apache
RUN apt-get update && apt-get install -y \
    && apt-get install -y libmcrypt-dev mariadb-client \
    && apt-get install -y zip unzip git vim

RUN docker-php-ext-install pdo_mysql session json mbstring
COPY php/ /var/www/html/

