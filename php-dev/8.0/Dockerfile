FROM digbang/php:8.0

LABEL version="1.0.0"
LABEL maintainer="Dario Govergun <dgovergun@digbang.com>, Mariano Filipoff <mfilipoff@digbang.com>"

# 1. SSL cert
RUN apt-get update && apt-get install -y ssl-cert

# 2. xdebug
RUN pecl install xdebug

# 3. composer, then require packages
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 4. clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# 5. copy extension config files
COPY conf.d /usr/local/etc/php/conf.d/
