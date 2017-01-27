FROM digbang/php:7.0

MAINTAINER Guido Contreras Woda <gcontreras@digbang.com>

RUN pecl install xdebug \
	&& php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini