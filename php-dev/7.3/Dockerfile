FROM digbang/php:7.3

LABEL version="1.0.0"
LABEL maintainer="Dario Govergun <dgovergun@digbang.com>"

# 1. SSL cert
RUN apt-get update && apt-get install -y ssl-cert

# 2. copy .ini files into conf.d directory
COPY conf.d/docker-php-ext-opcache.ini /usr/local/etc/php/conf.d/
COPY conf.d/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/

# 4. composer, then require packages
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN /usr/bin/composer global require hirak/prestissimo

# 5. clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
