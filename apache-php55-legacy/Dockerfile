FROM nimmis/apache:14.04

MAINTAINER Onirudda Odikare Jhalak <jhalak1983@gmail.com>

# Install necessities
RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    php5 libapache2-mod-php5  \
    php5-fpm php5-cli php5-mysqlnd php5-pgsql php5-sqlite php5-redis \
    php5-memcache mysql-client php5-xdebug \
    php5-apcu php5-intl php5-imagick php5-mcrypt php5-json php5-gd php5-curl memcached git && \
    php5enmod mcrypt

# Enable apache mods.
RUN a2enmod php5
RUN a2enmod rewrite
RUN a2enmod ssl

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Expose apache.
EXPOSE 80
EXPOSE 443

ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf
ADD ssl-config.conf /etc/apache2/sites-enabled/default-ssl.conf
ADD php.ini /etc/php5/apache2/php.ini

# By default start up apache in the foreground, override with /bin/bash for interative.
RUN service memcached start
CMD /usr/sbin/apache2ctl -D FOREGROUND
