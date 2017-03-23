FROM digbang/php:7.1

MAINTAINER Guido Contreras Woda <gcontreras@digbang.com>

RUN apt-get update \
	&& apt-get install -y ssl-cert \
	&& pecl install xdebug \
	&& docker-php-ext-install pcntl \
	&& php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
	&& rm -rf /var/lib/apt/lists/*

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini