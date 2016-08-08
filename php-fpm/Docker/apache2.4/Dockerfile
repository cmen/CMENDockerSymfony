FROM ubuntu:16.04

MAINTAINER Christophe Meneses

RUN apt-get update && apt-get install -y apache2

RUN a2enmod proxy_fcgi

ADD fpm.conf /etc/apache2/conf-enabled/

EXPOSE 80

WORKDIR /var/www/html

CMD /usr/sbin/apache2ctl -D FOREGROUND
