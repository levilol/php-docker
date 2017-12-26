FROM php:fpm
RUN curl -sS https://getcomposer.org/installer | php \
        && mv composer.phar /usr/local/bin/ \
        && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

COPY . /var/www/html

EXPOSE 9000

WORKDIR /var/www/html

RUN composer install --prefer-source --no-interaction
