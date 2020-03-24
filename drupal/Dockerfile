FROM php:7.2.19-fpm

RUN docker-php-ext-install pdo_mysql

RUN apt-get update && apt-get install zlib1g-dev -y \
        libmcrypt-dev \
        libpq-dev \
        libjpeg-dev \
        libfreetype6-dev \
        libpng-dev \
        xvfb libfontconfig wkhtmltopdf
RUN pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt \
    && docker-php-ext-install -j$(nproc) pdo \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) exif \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN apt-get update && apt-get install -y libicu-dev g++
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

RUN apt-get update && apt-get install -y --no-install-recommends \
      wget \
      gnupg \
      apt-utils \
      software-properties-common \
      build-essential \
      mysql-client \
      python3-dev; \
    apt-get update && apt-get install -y openssl curl git;

RUN docker-php-ext-install mysqli

# Install composer
ADD ./code /app/code/

WORKDIR /app/code/

RUN rm -r /var/lib/apt/lists/* ; \
    rm -Rf /tmp/*

# USER root