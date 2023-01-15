### ОПИСАНИЕ
- это моя шпаргалка для поднятия локального сервера в докере для работы Laravel
- содержит в себе настройки:
  - docker
  - nginx
  - mysql
  - php
  - xdebug
  - laravel

### Установка
В нужной папке выполнить:
```
git clone https://github.com/rchitector/docker_nginx_php_mysql_xdebug_laravel.git .
```
Чтобы сразу удалить ненужные данные .git, можно выполнить команду:
```
rm -rf !$/.git && rm ./.gitignore
```

### ОКРУЖЕНИЕ
- скопировать файл **.env.example** в файл с именем **.env**

### xxxxxxxxxxx
- придумать название проекта в нижнем регистре без пробелов (например my_project)
- заменить все упоминания **xxxxxxxxxxx** на название проекта
- заменить все настройки в файле .env (DATABASE_PASSWORD, DATABASE_NAME, DATABASE_USER) на нужные

### Docker
- запуск службы докера:
```
sudo systemctl start docker.service && sudo systemctl start docker.socket
```
- остановка службы докера:
```
sudo systemctl stop docker.service && sudo systemctl stop docker.socket
```

### DB - база данных
- логи БД лежат в папке: **docker/db/logs**
- все данные БД лежат в папке: **docker/db/data**

### NGINX - сервер
- настройки лежат в файле **docker/nginx/conf.d/nginx.conf**
- логи сервера лежат в папке **docker/nginx/logs**

### PHP - интерпритатор
- настройки контейнера лежат в файле **docker/php-fpm/Dockerfile**
- настройки **PHP** лежат в файле **docker/php-fpm/php-overrides.ini**

### Xdebug + PhpStorm
- в настройках PhpStorm: PHP > Servers
- в поле Host указать название хоста точно такое же как и в настройках **docker/nginx/conf.d/nginx.conf** > server > server_name
- не забыть добавить так же этот хост в файле /etc/hosts (например строку "127.0.0.1 localhost" где localhost - это название из server_name)
- поставить галочку Use path mappings
- указать корень локальной папки и корневой папки внутри сервера.
- в данном случае для папки source нужно указать /app (что соответствует настройкам в docker-compose.yml xxxxxxxxxxx_php-fpm > volumes > "./source:/app")
- в меню Run активировать пункт Start Listening for PHP Debug connection
- ставим точку останова в коде и можно пробовать открывать страницу
<!-- вот тут урок https://www.youtube.com/watch?v=7YuYxbYd3P0 -->

### Установка Laravel
- в корне проекта выполнить:
```
git clone https://github.com/laravel/laravel.git ./source
```
Чтобы сразу удалить ненужные данные .git, можно выполнить команду:
```
rm -rf ./source/.git && rm ./source/.gitignore
```

- скопировать данные настройки БД из файла **.env** в файл **./source/.env**
- в файле **./source/.env** заменить **DB_HOST=127.0.0.1** на **DB_HOST=xxxxxxxxxxx_db** чтобы соединение с БД смотрело в контейнер
- выполнить команду **docker exec -it xxxxxxxxxxx_php_container bash**
- **xxxxxxxxxxx_php_container** - это имя контейнера, изменить которое можно в файле **docker-compose.yml**
- внутри контейнера выполнить команду **composer install**
- внутри контейнера выполнить команду **php artisan key:generate**
- внутри контейнера выполнить команду **php artisan migrate**

### Tests
- выполнить команду в терминале: **docker exec -t  xxxxxxxxxxx_php_container php artisan test**

### Chrome
- иногда после изменения конфигурации nginx браузер не хочет обновлять редиректы. Один из вариантов это очистить кэш браузера (Ctrl + Shift + Del). 