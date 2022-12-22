**ОКРУЖЕНИЕ**
- скопировать файл **.env.example** в файл с именем **.env**

**MARIADB** - база данных
- в файле **.env** в разделе **database** заменить все **CHANGE_ME** на нужные значения
- логи БД лежат в папке: **docker/mariadb/logs**
- все данные БД лежат в папке: **docker/mariadb/data**

**NGINX** - сервер
- настройки лежат в файле **docker/nginx/nginx.conf**
- логи сервера лежат в папке **docker/nginx/logs**

**PHP** - интерпритатор
- настройки контейнера лежат в файле **docker/php-fpm/Dockerfile**
- настройки **PHP** лежат в файле **docker/php-fpm/php-overrides.ini**

**Установка LARAVEL**
- в корне проекта выполнить **git clone https://github.com/laravel/laravel.git ./source**
- скопировать данные настройки БД из файла **.env** в файл **./source/.env**
- в файле **./source/.env** заменить **DB_HOST=127.0.0.1** на **DB_HOST=mariadb** чтобы соединение с БД смотрело в контейнер
- выполнить команду **docker exec -it php_container bash**
- **php_container** - это имя контейнера, изменить которое можно в файле **docker-compose.yml**
- внутри контейнера выполнить команду **composer install**
- внутри контейнера выполнить команду **php artisan key:generate**
- внутри контейнера выполнить команду **php artisan migrate**