FROM php:7.3-apache-stretch

MAINTAINER Onirudda Odikare Jhalak <jhalak1983@gmail.com>

RUN apt-get update -y \
    && apt-get install -y zlib1g-dev libpng-dev libpq-dev libzip-dev libmcrypt-dev mysql-client vim git wget \
    && rm -rf /var/lib/apt/lists/* \
    && pecl install redis-4.0.1 \
    && docker-php-ext-enable redis

# Install zip
RUN docker-php-ext-install mysqli pdo zip pdo_mysql pdo_pgsql gd

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install phpunit
RUN wget https://phar.phpunit.de/phpunit-8.3.5.phar \
	&& chmod u+x phpunit-8.3.5.phar \
    && mv phpunit-8.3.5.phar /usr/local/bin/phpunit

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2

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
