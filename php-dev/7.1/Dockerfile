FROM digbang/php:7.1

MAINTAINER Dario Govergun <dgovergun@digbang.com>

RUN apt-get update \
	&& apt-get install -y ssl-cert \
	&& pecl install xdebug \
	&& docker-php-ext-install pcntl \
	&& php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
	&& /usr/bin/composer global require hirak/prestissimo \
	&& rm -rf /var/lib/apt/lists/*

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
