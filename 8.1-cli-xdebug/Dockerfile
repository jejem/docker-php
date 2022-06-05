FROM jejem/php:8.1-cli
MAINTAINER Jérémy "Jejem" Desvages <jejem@phyrexia.org>

RUN set -eux; \
    pecl install xdebug; \
    docker-php-ext-enable \
        xdebug \
    ;
