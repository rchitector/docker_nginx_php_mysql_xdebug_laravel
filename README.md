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
