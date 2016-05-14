FROM ubuntu:15.10

MAINTAINER Christophe Meneses

RUN echo "deb http://ppa.launchpad.net/ondrej/php5-5.6/ubuntu wily main" | tee -a /etc/apt/sources.list \ 
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C \ 
    && apt-get update

RUN apt-get install -y apache2 

RUN apt-get install -y php5-common php5-cli libapache2-mod-php5

RUN apt-get install -y php5-mcrypt php5-mysql php5-apcu php5-curl php5-intl php5-xdebug

ADD php-custom.ini /etc/php5/apache2/conf.d
ADD 20-xdebug.ini /etc/php5/apache2/conf.d
ADD php-custom.ini /etc/php5/cli/conf.d
ADD 20-xdebug.ini /etc/php5/cli/conf.d

RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer

RUN apt-get install -y git

EXPOSE 80

WORKDIR /etc/php5

CMD /usr/sbin/apache2ctl -D FOREGROUND
