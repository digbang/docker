FROM digbang/php:7.2

LABEL version="1.0.0"
LABEL maintainer="Dario Govergun <dgovergun@digbang.com>"

# 1. SSL cert
RUN apt-get update && apt-get install -y ssl-cert

# 2. composer, then require packages
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN /usr/bin/composer global require hirak/prestissimo

# 3. clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# 4. copy extension config files
COPY conf.d /usr/local/etc/php/conf.d/
