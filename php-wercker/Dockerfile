FROM php:5.6-cli

MAINTAINER Kyle Shenk k.shenk@gmail.com

## update repo
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libbz2-dev \
    php-pear \
    curl \
    wget \
    git \
	libicu-dev \
    && docker-php-ext-install iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

## Set memory limit
RUN echo "memory_limit=1024M" > /usr/local/etc/php/conf.d/memory-limit.ini

## Set date.timezone in php.ini - both of them...
RUN sed -i "s/^\;date\.timezone.*$/date\.timezone = \"America\/New_York\" /g" /etc/php5/cli/php.ini
RUN echo "date.timezone = \"America/New_York\"" > /usr/local/etc/php/conf.d/date-timezone.ini

## Set environmental variables
ENV COMPOSER_HOME /root/composer

## Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN docker-php-ext-install \
    zip \
    bz2 \
    mbstring \
    pdo_mysql \
    intl

## Install phpunit
RUN wget https://phar.phpunit.de/phpunit.phar && \
    chmod +x phpunit.phar && \
    mv phpunit.phar /usr/local/bin/phpunit
