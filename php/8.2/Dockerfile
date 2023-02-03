FROM php:8.2-fpm-alpine

LABEL version="1.0.0"
LABEL maintainer="Dario Govergun <dgovergun@digbang.com>, Mariano Filipoff <mfilipoff@digbang.com>"

# Essentials
RUN echo "UTC" > /etc/timezone

RUN apk add --no-cache \
    freetype-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    libxml2-dev \
    autoconf \
    g++ \
    imagemagick-dev \
    libtool \
    make \
    curl \
    sqlite \
    mysql-dev \
    postgresql-dev \
    libzip-dev \
    p7zip

# Installing bash
RUN apk add bash
RUN sed -i 's/bin\/ash/bin\/bash/g' /etc/passwd

# Installing PECL
RUN pecl install redis

# Configure PHP
RUN mkdir -p /run/php/
RUN touch /run/php/php8.2-fpm.pid

# Configure PHP extensions
RUN docker-php-ext-install pdo pdo_pgsql pdo_mysql pgsql zip exif gd
RUN docker-php-ext-enable pdo pdo_pgsql pdo_mysql redis exif

# Clear APK cache
RUN rm -rf /var/cache/apk/*
