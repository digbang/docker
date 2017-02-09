FROM digbang/php:7.1

MAINTAINER Guido Contreras Woda <gcontreras@digbang.com>

RUN pecl install xdebug \
	&& docker-php-ext-install pcntl \
	&& php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini