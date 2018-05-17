FROM php:7.1-apache

MAINTAINER Dario Govergun <dgovergun@digbang.com>

ENV DEPENDENCIES \
	imagemagick \
    libfreetype6 \
    libjpeg62-turbo \
    libpng12-0

ENV BUILD_PACKAGES \
    libcurl4-openssl-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg-dev \
    libjpeg62-turbo-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    libmemcached-dev \
    libncurses5-dev \
    libpng-dev \
    libpng12-dev \
    libpq-dev \
    libtidy-dev \
    libxml2-dev \
    libz-dev \
    locales \
    locales-all \
    zlib1g-dev

RUN apt-get update \
    && apt-get install -y $DEPENDENCIES $BUILD_PACKAGES \
    && docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib/x86_64-linux-gnu \
        --with-png-dir=/usr/lib/x86_64-linux-gnu \
        --with-freetype-dir=/usr/lib/x86_64-linux-gnu \
    && docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install -j$(nproc) mcrypt \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) pdo_pgsql \
    && docker-php-ext-install -j$(nproc) soap \
    && docker-php-ext-install -j$(nproc) tidy \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-configure intl \
    && pecl install imagick \
    && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/imagick.ini \
    && apt-get remove -y $BUILD_PACKAGES \
    && rm -rf /var/lib/apt/lists/*

RUN a2enmod ssl rewrite
