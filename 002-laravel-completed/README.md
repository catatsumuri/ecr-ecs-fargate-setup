

```
docker build -t my-ecs-php-fpm -f ./srv/Dockerfile --target=php-fpm . 
docker build -t my-ecs-nginx -f ./srv/Dockerfile --target=nginx . 
docker-compose down
docker-compose up -d
```
