FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

# Don't really need supervisor here, but was trying it out.
RUN apt-get update && apt-get install -y apache2 supervisor
RUN mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/supervisor

RUN a2enmod status
RUN a2enmod socache_memcache
RUN a2enmod ssl

RUN mkdir /etc/apache2/ssl
COPY apache.key /etc/apache2/ssl/apache.key
COPY apache.crt /etc/apache2/ssl/apache.crt
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
COPY ssl.conf /etc/apache2/mods-available/ssl.conf
COPY index.html /var/www/html/index.html

RUN a2ensite default-ssl.conf

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80 443
CMD ["usr/bin/supervisord"]

