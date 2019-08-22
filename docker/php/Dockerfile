#FROM debian
FROM php:7.2-fpm
ARG COMPOSER_HOME=/.composer
ENV COMPOSER_HOME ${COMPOSER_HOME}

RUN docker-php-ext-install pdo_mysql

RUN apt-get update && apt-get install -y wget \
    git \
    zip

RUN wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer --quiet

RUN pecl install xdebug \
&& docker-php-ext-enable xdebug \
&& echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
&& echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

WORKDIR /var/www/symfony

RUN mkdir -p $COMPOSER_HOME && chmod 777 -R $COMPOSER_HOME

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

#CMD ["php-fpm", "--allow-to-run-as-root"]
