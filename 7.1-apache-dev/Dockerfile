FROM elendev/infomaniak-php:7.1-apache

RUN pecl install xdebug-2.5.0 && \
    docker-php-ext-enable xdebug && \
    echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

RUN apt-get update && \
    apt-get install ssl-cert && \
    rm -rf /var/lib/apt/lists/* && \
    a2ensite default-ssl && \
    a2enmod ssl && \
    service apache2 restart