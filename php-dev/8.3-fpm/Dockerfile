FROM digbang/php:8.3-fpm

LABEL version="1.0.0"
LABEL maintainer="Dario Govergun <dgovergun@digbang.com>, Mariano Filipoff <mfilipoff@digbang.com>"

# Copy PHP configuration files
COPY ./conf.d/ "$PHP_INI_DIR/conf.d/"

# Install PHP extensions
RUN install-php-extensions xdebug @composer-2