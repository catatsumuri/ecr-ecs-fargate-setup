FROM php:8.4-fpm

WORKDIR /srv

COPY ./laravel-app /srv

RUN chown www-data storage database -R
RUN cp .env.example .env

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip

COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN composer install

EXPOSE 9000
