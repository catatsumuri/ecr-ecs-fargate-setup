# --------------------------------------
# Stage 1: frontend build stage
# --------------------------------------
FROM node:18-alpine AS frontend-builder

WORKDIR /laravel

COPY ./laravel-app /laravel

RUN npm install && npm run build
RUN mkdir /public && cp -a public/* /public

# --------------------------------------
# Stage 2: PHP-FPM
# --------------------------------------
FROM php:8.4-fpm AS php-fpm

WORKDIR /srv

COPY ./laravel-app /srv
COPY --from=frontend-builder /public /srv/public

RUN cp .env.example .env
RUN chown -R www-data:www-data storage database

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip

COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN composer install

EXPOSE 9000

# --------------------------------------
# Stage 3: Nginx
# --------------------------------------
FROM nginx:alpine AS nginx

WORKDIR /usr/share/nginx/html

COPY ./srv/default.conf /etc/nginx/conf.d/default.conf
COPY --from=php-fpm /srv/public/ /usr/share/nginx/html

EXPOSE 80
