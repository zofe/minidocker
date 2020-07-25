FROM php:7.4-fpm-alpine

RUN apk add --no-cache \
    bash \
    nano

#RUN docker-php-ext-configure xxxxx
RUN docker-php-ext-install pdo pdo_mysql

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


COPY ./php-ini-overrides.ini /usr/local/etc/php/conf.d/custom.ini

RUN apk --no-cache add shadow && usermod -u 1000 www-data && groupmod -g 1000 www-data


WORKDIR /application

#RUN chown -R www-data:www-data /application/storage/logs

