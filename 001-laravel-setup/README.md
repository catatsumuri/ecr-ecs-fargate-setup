RUN 

```
docker build -t my-ecs-nginx -f ./nginx/Dockerfile . --no-cache
docker build -t my-ecs-php-fpm -f ./php-fpm/Dockerfile . --no-cache
docker-compose down
docker-compose up -d
```
