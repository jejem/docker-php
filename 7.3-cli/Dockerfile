FROM php:7.3-cli
MAINTAINER Jérémy "Jejem" Desvages <jejem@phyrexia.org>

RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        locales \
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
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"; \
    php composer-setup.php --install-dir="/usr/local/bin"; \
    ln -s composer.phar /usr/local/bin/composer; \
    php -r "unlink('composer-setup.php');"
