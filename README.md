## Oksana Bürki
<https://xeniaweb.art>

### About this project

Start Docker for PHP Projects with PostgreSQL, Nginx, Redis, Nodejs
##
### php-fpm 8.3 image for php projects
Includes:
* bcmath
* gd
* intl
* pcntl
* ldap
* pdo_mysql
* pdo_pgsql
* zip
* memcached
* redis
* xdebug
* composer

[//]: # (Команды, выполняемые внутри контейнеров)

[//]: # (## Установка npm/composer)
[//]: # (docker compose run --rm node npm ci)
[//]: # (docker compose exec -it raifpartners-app composer install)

[//]: # (## Установка пакетов npm/composer)
[//]: # (docker compose run --rm node npm install gocpa/blablablapackage)
[//]: # (docker compose exec -it raifpartners-app composer require gocpa/blablablapackage)

[//]: # (## Сборка фронтенда)
[//]: # (docker compose run --rm node npm run build)
[//]: # (docker compose run --rm --service-ports node npm run dev)
