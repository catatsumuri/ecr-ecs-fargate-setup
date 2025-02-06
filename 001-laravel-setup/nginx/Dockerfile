FROM nginx:alpine

WORKDIR /usr/share/nginx/html

COPY ./laravel-app/public /usr/share/nginx/html

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
