FROM jejem/php:8.1-fpm
MAINTAINER Jérémy "Jejem" Desvages <jejem@phyrexia.org>

RUN set -eux; \
    pecl install xdebug; \
    docker-php-ext-enable \
        xdebug \
    ;
