# Would you like to use another custom folder than $ZSH/custom?
FROM php:7.0.8-fpm-alpine
MAINTAINER ChasonTang <chasontang@gmail.com>

ENV PG_VERSION 9.5.3-r1

RUN apk add --no-cache postgresql-dev=$PG_VERSION \
    && docker-php-ext-install do_pgsql \
    && apk del --no-cache postgresql-dev=$PG_VERSION \
    && apk add --no-cache postgresql-libs=$PG_VERSION \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"