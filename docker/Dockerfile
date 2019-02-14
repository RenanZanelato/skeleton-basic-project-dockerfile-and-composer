FROM php:7.2-apache

EXPOSE 9000

RUN apt-get update

RUN apt-get install -y libpq-dev && \
    apt-get install -y libpng-dev && \
    apt-get install -y zip unzip && \
    docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql && \
    docker-php-ext-install pdo pdo_pgsql pgsql && \
    docker-php-ext-install gd

RUN apt-get install -y libxml2-dev && \
    docker-php-ext-install soap

RUN curl -sSk https://getcomposer.org/installer | php -- --disable-tls && \
	mv composer.phar /usr/local/bin/composer

RUN a2enmod rewrite

RUN apt-get update \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_host=${xdebugip}" >> /usr/local/etc/php/conf.d/xdebug.ini

ENV APACHE_DOCUMENT_ROOT /var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-enabled/*.conf