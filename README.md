# DNMP环境
## PHP
> 基于 php：7.3-fpm-alpine
>
> nginx 当前最新版
>
> 操作
>
>


#举个例子(laravel)
```
docker-compose exec php composer create-project --prefer-dist laravel/laravel blog

docker-compose run node `cd blog &&  yarn install`

