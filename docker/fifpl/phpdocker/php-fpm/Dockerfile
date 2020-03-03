FROM phpdockerio/php7-fpm:latest
WORKDIR "/application"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php-memcached php-mysql php-gd php-intl php-ldap php-soap php-xdebug \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

ADD xdebug.ini /etc/php/7.0/cli/conf.d/20-xdebug.ini
ADD xdebug.ini /etc/php/7.0/fpm/conf.d/20-xdebug.ini
