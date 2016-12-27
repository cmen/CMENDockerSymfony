FROM ubuntu:16.10

MAINTAINER Christophe Meneses

# Installation PHP + extensions
RUN apt-get update && apt-get install -y \
    php-fpm \
    php-mcrypt \
    php-mysql \
    php-apcu \
    php-curl \
    php-intl \
    php-xdebug \
    php-xml \
    php-zip

# Configuration PHP (FPM, CLI) + extensions
COPY config/etc/php/7.0/fpm/php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf
COPY config/etc/php/7.0/fpm/pool.d/www.conf /etc/php/7.0/fpm/pool.d/www.conf

COPY config/etc/php/7.0/mods-available/php-custom.ini /etc/php/7.0/mods-available/php-custom.ini
RUN ln -s /etc/php/7.0/mods-available/php-custom.ini /etc/php/7.0/fpm/conf.d/php-custom.ini
RUN ln -s /etc/php/7.0/mods-available/php-custom.ini /etc/php/7.0/cli/conf.d/php-custom.ini

# La config de xdebug est automatiquement ajoutée dans fpm et cli
COPY config/etc/php/7.0/mods-available/xdebug.ini /etc/php/7.0/mods-available/xdebug.ini

# Installation utilitaires
RUN apt-get install -y git iproute2 vim

# Installation de composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

WORKDIR /var/www/html

EXPOSE 9000

RUN service php7.0-fpm start

CMD php-fpm7.0 -F

