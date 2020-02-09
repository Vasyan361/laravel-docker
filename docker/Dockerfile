FROM php:7.4-apache-buster

RUN docker-php-ext-install pdo_mysql \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && a2enmod rewrite

COPY . /var/www/html
COPY docker/vhost.conf /etc/apache2/sites-available/000-default.conf
COPY docker/config/php/conf.d/*.ini /usr/local/etc/php/conf.d
COPY docker/start.sh /user/local/bin/start
COPY docker/config/php/php.ini /usr/local/etc/php

RUN chown -R www-data:www-data /var/www/html \
    && chmod +x /user/local/bin/start

CMD ["/user/local/bin/start"]
