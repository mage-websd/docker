FROM php:8.0.2-fpm

ARG nginx_folder=build_setup/nginx_proxy/nginx/
ARG php_folder=build_setup/php/

RUN mkdir -p /app/code/
RUN mkdir -p /app/run/

WORKDIR /app/code/

# Install dependencies
RUN apt update && apt install -y \
    build-essential \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libzip-dev \
    locales \
    jpegoptim \
    optipng \
    pngquant \
    gifsicle \
    zip \
    unzip\
    autoconf \
    zlib1g-dev

RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl bcmath gd
RUN pecl install grpc && docker-php-ext-enable grpc

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY ./source_code/ /app/code/
RUN composer install --no-dev

#### for dev env
# EXPOSE 9000
# CMD ["php-fpm"]

### install nginx
RUN apt update -y && apt install nginx -y
RUN mkdir -p /etc/nginx/sites-available/
COPY ${nginx_folder}nginx.conf /etc/nginx/nginx.conf
COPY ${nginx_folder}stage/sites/ /etc/nginx/sites-available/
COPY ${nginx_folder}/sd.conf /etc/nginx/sd.conf

# COPY ${php_folder}/php-fpm.d/www.conf /usr/local/etc/php-fpm.d/www.conf

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

EXPOSE 80
CMD ["sh", "-c",  "php-fpm -DR; nginx -g 'daemon off;'"]
