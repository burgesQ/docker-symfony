# See https://github.com/docker-library/php/blob/master/7.1/fpm/Dockerfile
FROM php:7.1-fpm
ARG TIMEZONE

MAINTAINER Maxence POUTORD <maxence.poutord@gmail.com>

RUN apt-get update && apt-get install -y \
    openssl \
    git \
    zsh \
    emacs \
    unzip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone
RUN printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql

# Install zsh and prezto
RUN cd ~ ; \
    git clone -b phpFpm --single-branch --recursive https://github.com/burgesQ/prezto ~/.zprezto ; \
    cd ./.zprezto ; \
    ./install

RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

# run cimposer as root
ENV COMPOSER_ALLOW_SUPERUSER 1

WORKDIR /var/www/symfony
