FROM ubuntu:14.04
MAINTAINER Alexander Schenkel <alex@alexi.ch>

VOLUME ["/var/www"]

RUN apt-get update && \
    apt-get install -y \
      apache2 \
      php5 \
      php5-cli \
      libapache2-mod-php5 \
      php5-gd \
      php5-json \
      php5-ldap \
      php5-mysql \
      php5-pgsql \
      php5-memcache \
      mysql-client \
      php5-xdebug \
      php5-apcu \
      php5-intl \
      php5-imagick \
      php5-mcrypt \
      php5-json \
      php5-gd \
      php5-curl \
      memcached \
      git && \
      php5enmod mcrypt

COPY apache_default /etc/apache2/sites-available/000-default.conf
COPY run /usr/local/bin/run
RUN chmod +x /usr/local/bin/run
RUN a2enmod rewrite

EXPOSE 80
CMD ["/usr/local/bin/run"]
