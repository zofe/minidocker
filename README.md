## Minidocker 

minimal docker setup for PHP development (i.e. Laravel projects),
it start from alpine images:   
- nginx(1.13)  
- php-fpm (7.4)
- mariadb (latest)

The idea is to keep all images really small and ready to run on small basic vps:

```
.. minidocker_nginx      ..  20.8 MB  
.. minidocker_mariadb_   ..  37.3 MB
.. minidocker_php-fpm    ..  90 MB
```

### configurations
copy and paste __.env.example__ to __.env__ and change as you need
```.dotenv
COMPOSE_PROJECT_NAME=minidocker
COMPOSE_FILE=docker-compose.yml

VIRTUAL_HOST=minidocker.local
EMAIL=me@minidocker.local
PROXY_NETWORK=nginx-proxy

MYSQL_BIND_PORT=33060
NGNIX_BIND_PORT=80

NGINX_TEMPLATE=docker/nginx/nginx.conf

LETSENCRYPT_HOST="${VIRTUAL_HOST}"
LETSENCRYPT_EMAIL="${EMAIL}"

DB_DATABASE=minidocker_db
DB_USERNAME=minidocker
DB_PASSWORD=minidocker
DB_ROOT_PASSWORD=root

```



### usage

- fork or download the repo 
- then raise docker containers (nginx, php, mariadb)

```
docker-compose up -d
```

- then enter in php-fpm container

```
docker-compose exec php-fpm bash
```

- you can run a simple phpinfo() 
```
mkdir public && echo '<?php phpinfo();' > /application/public/index.php && chown -R www-data.www-data /application/public/

```
- you can download, install and run laravel 

```
composer create-project --prefer-dist laravel/laravel /application
chown -R www-data.www-data /application

```
If you use laravel edit the default /application/.env to match your DB config ie:
```dotenv
...
DB_HOST=mariadb
DB_PORT=3306
DB_DATABASE=minidocker_db
DB_USERNAME=minidocker
DB_PASSWORD=minidocker
...
```
 

You should be ready to develop your app in __/application__

You can define in application a "submodule" or just instance a new git project with your web application.
 




### production

I also added a .env.prod as alternative to .env.example for "production" or "stage" servers.  
It's useful for:

- use https instead http (with a real hostname... Let's Encrypt certificate etc..)
- use a different network for containers (I usually usa a nginx reverse proxy) 
- different port mapping 


bye Felice
