FROM php:7.2-fpm-buster

LABEL Name="nmoeini/php:7.2-fpm-apcu-buster" Mainteiner="Navid Moeini <nmoeini@tmhcc.com>" Version="0.1"

#INSTALL APCU
ARG APCU_VERSION=5.1.11
RUN set -eux \
	&& savedAptMark="$(apt-mark showmanual)" \
	&& apt-get update \
	&& apt-get install -y \
	    g++ \
    && pecl install apcu-${APCU_VERSION} \
    && pecl install apcu_bc \
    && docker-php-ext-enable apcu \
    && echo "extension=apcu.so" >> /usr/local/etc/php/php.ini \
    && echo "apc.enable_cli=1" >> /usr/local/etc/php/php.ini \
    && echo "apc.enable=1" >> /usr/local/etc/php/php.ini \
##  Clear cache \
##  -----------------------------------------------------------------------  ## \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && php --ini \
    && php --info | grep apc
#APCU

CMD ["php-fpm"]