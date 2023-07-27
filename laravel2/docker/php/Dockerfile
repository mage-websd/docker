FROM public.ecr.aws/docker/library/php:8.1-fpm-alpine

ARG TZ

WORKDIR /code

RUN set -eux
RUN apk update && apk add --no-cache g++ libtool composer npm make libzip-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libxml2-dev

RUN apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS

RUN if [ ${INSTALL_PHPREDIS} = true ]; then \
    printf "\n" | curl 'http://pecl.php.net/get/redis-4.1.1.tgz' -o redis-4.1.1.tgz \
    && pecl install redis-4.1.1.tgz \
    &&  rm -rf redis-4.1.1.tgz \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis \
;fi

RUN docker-php-ext-configure opcache --enable-opcache
RUN docker-php-ext-install opcache bcmath pdo_mysql exif zip
RUN apk del autoconf g++ libtool make
RUN apk add linux-headers
RUN apk add php-tokenizer php-gd php-dom php-session php-fileinfo php-xml php-xmlreader php-xmlwriter php-simplexml

ADD . .
ADD ./docker/php/php.ini /usr/local/etc/php/php.ini

CMD ["php-fpm","-F"]
