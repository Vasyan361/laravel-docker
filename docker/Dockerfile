FROM php:7.4-fpm

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS=0 \
    PHP_OPCACHE_MAX_ACCELERATED_FILES=9000 \
    PHP_OPCACHE_MEMORY_CONSUMPTION=128

RUN apt-get update -yqq \
    && apt-get install -y --no-install-recommends \
        nginx \
        supervisor \
        procps \
    && docker-php-ext-install pdo_mysql \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug opcache

ADD . /var/www/html
ADD docker/config/php/conf.d/*.ini /usr/local/etc/php/conf.d/
ADD docker/config/php/php.ini /usr/local/etc/php
ADD docker/config/supervisor/supervisord.conf /etc/supervisor
ADD docker/config/nginx/default /etc/nginx/sites-available/
ADD docker/config/nginx/h5bp/ /etc/nginx/h5bp
ADD docker/config/php/php-fpm.d/docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf
ADD docker/start.sh /user/local/bin/start

RUN chown -R www-data:www-data /var/www/html \
    && chmod +x /user/local/bin/start \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

CMD ["/user/local/bin/start"]
