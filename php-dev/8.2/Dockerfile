FROM digbang/php:8.2

LABEL version="1.0.0"
LABEL maintainer="Dario Govergun <dgovergun@digbang.com>, Mariano Filipoff <mfilipoff@digbang.com>"

# xdebug
RUN apk add --update linux-headers \
    && pecl install xdebug

# Composer install
COPY --from=composer:2.5 /usr/bin/composer /usr/bin/composer

# Setup www-data user
RUN apk add shadow && usermod -u 1000 www-data && groupmod -g 1000 www-data
RUN chown -R www-data:www-data ./
