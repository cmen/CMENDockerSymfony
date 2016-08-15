FROM ubuntu:16.04

MAINTAINER Christophe Meneses

# PHP + extensions installation
RUN apt-get update && apt-get install -y \
    php-fpm \
    php-mcrypt \
    php-mysql \
    php-apcu \
    php-curl \
    php-intl \
    php-xdebug \
    php-xml

# PHP (FPM, CLI) + extensions configuration
COPY config/etc/php/7.0/fpm/php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf
COPY config/etc/php/7.0/fpm/pool.d/www.conf /etc/php/7.0/fpm/pool.d/www.conf

COPY config/etc/php/7.0/mods-available/php-custom.ini /etc/php/7.0/mods-available/php-custom.ini
RUN ln -s /etc/php/7.0/mods-available/php-custom.ini /etc/php/7.0/fpm/conf.d/php-custom.ini
RUN ln -s /etc/php/7.0/mods-available/php-custom.ini /etc/php/7.0/cli/conf.d/php-custom.ini

COPY config/etc/php/7.0/mods-available/xdebug.ini /etc/php/7.0/mods-available/xdebug.ini
RUN ln -s /etc/php/7.0/mods-available/xdebug.ini /etc/php/7.0/fpm/conf.d/xdebug.ini
RUN ln -s /etc/php/7.0/mods-available/xdebug.ini /etc/php/7.0/cli/conf.d/xdebug.ini

# Utils
RUN apt-get install -y iproute2

WORKDIR /var/www/html

EXPOSE 9000

RUN service php7.0-fpm start

CMD php-fpm7.0 -F

