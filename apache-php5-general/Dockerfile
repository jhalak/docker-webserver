FROM php:5.6-apache-stretch

MAINTAINER Onirudda Odikare Jhalak <jhalak1983@gmail.com>

RUN apt-get update -y \
    && apt-get install -y zlib1g-dev libmemcached-dev memcached mysql-client vim git \
    && rm -rf /var/lib/apt/lists/* \
    && pecl install redis-2.2.8 \
    && pecl install memcache \
    && pecl install xdebug-2.5.3 \
    && docker-php-ext-enable redis memcache xdebug

# Install zip
RUN docker-php-ext-install mysqli pdo pdo_mysql zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Define PHP_TIMEZONE env variable
ENV PHP_TIMEZONE Asia/Dhaka

# Configure Apache Document Root
ENV APACHE_DOC_ROOT /var/www/html

# Enable Apache mod_rewrite
RUN a2enmod rewrite
RUN a2enmod ssl

# Additional PHP ini configuration
COPY ./php.ini /usr/local/etc/php/conf.d/999-php.ini

COPY start.sh /usr/local/bin/start
RUN chmod +x /usr/local/bin/start

CMD ["/usr/local/bin/start"]