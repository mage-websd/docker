FROM php:7

RUN apt-get update -y && apt-get install -y openssl zip unzip git

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN docker-php-ext-install pdo mbstring

WORKDIR /a2/laravel
# COPY . /a2

# RUN composer create-project --prefer-dist laravel/laravel first
RUN cd /a2/laravel && composer install

CMD php /a2/laravel/artisan serve --host=0.0.0.0 --port=8181
# CMD php -S 0.0.0.0:8181
EXPOSE 8181
