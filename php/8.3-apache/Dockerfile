FROM php:8.3-apache

LABEL version="1.0.0"
LABEL maintainer="Dario Govergun <dgovergun@digbang.com>, Mariano Filipoff <mfilipoff@digbang.com>"

ENV TZ=UTC

# Set the timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Copy additional PHP configuration files
COPY ./conf.d/ "$PHP_INI_DIR/conf.d/"

# Set PHP configuration file
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

# Add script for installing PHP extensions
ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# Install basic PHP extensions
RUN install-php-extensions \
    bcmath \
    exif \
    opcache \
    pcntl \
    intl

# Install image manipulation PHP extension
RUN install-php-extensions \
    gd

# Install database-related PHP extensions
RUN install-php-extensions \
    pdo_mysql \
    pdo_pgsql

# Install caching-related PHP extension
RUN install-php-extensions \
    redis

# Install web service-related PHP extensions
RUN install-php-extensions \
    soap \
    sockets

# Install data processing-related PHP extensions
RUN install-php-extensions \
    tidy \
    zip

# Configure user www-data
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# Set ownership of web root directory to www-data
RUN chown -R www-data:www-data /var/www/html

# Set working directory
WORKDIR /var/www/html