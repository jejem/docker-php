FROM php:5.6-cli
MAINTAINER Jérémy "Jejem" Desvages <jejem@phyrexia.org>

RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        git \
        libcurl4-openssl-dev \
        libfreetype6-dev \
        libicu-dev \
        libjpeg62-turbo-dev \
        libmagickwand-dev \
        libmemcached-dev \
        libpng-dev \
        libzip-dev \
        libzstd-dev \
        locales \
        unzip \
        zlib1g-dev \
    ; \
    rm -rf /var/lib/apt/lists/*

RUN set -eux; \
    echo "en_GB ISO-8859-1" > /etc/locale.gen; \
    echo "en_GB.ISO-8859-15 ISO-8859-15" >> /etc/locale.gen; \
    echo "en_GB.UTF-8 UTF-8" >> /etc/locale.gen; \
    echo "fr_FR ISO-8859-1" >> /etc/locale.gen; \
    echo "fr_FR@euro ISO-8859-15" >> /etc/locale.gen; \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen; \
    echo "LANG=\"fr_FR.UTF-8\"" > /etc/default/locale; \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales

RUN set -eux; \
    rm -f /etc/localtime; \
    cp -f /usr/share/zoneinfo/Europe/Paris /etc/localtime; \
    echo "Europe/Paris" > /etc/timezone; \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure tzdata

RUN set -eux; \
    ln -s /usr/local/bin/php /usr/bin/php; \
    ln -s php.ini-production "$PHP_INI_DIR/php.ini"; \
    docker-php-ext-enable opcache

RUN set -eux; \
    docker-php-ext-configure curl; \
    docker-php-ext-configure gd --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib-dir; \
    docker-php-ext-configure gettext; \
    docker-php-ext-configure intl; \
    docker-php-ext-configure mysqli; \
    docker-php-ext-configure pdo_mysql; \
    docker-php-ext-configure zip; \
    docker-php-ext-install \
        curl \
        gd \
        gettext \
        intl \
        mysqli \
        pdo_mysql \
        zip \
    ;

RUN set -eux; \
    pecl install apcu-4.0.11; \
    pecl install igbinary-2.0.8; \
    pecl install imagick; \
    pecl install memcached-2.2.0; \
    pecl install msgpack-0.5.7; \
    pecl install redis-4.3.0; \
    docker-php-ext-enable \
        apcu \
        igbinary \
        imagick \
        memcached \
        msgpack \
        redis \
    ;

RUN set -eux; \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"; \
    php composer-setup.php --install-dir="/usr/local/bin"; \
    ln -s composer.phar /usr/local/bin/composer; \
    php -r "unlink('composer-setup.php');"
