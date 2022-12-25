FROM php:8.1-fpm
WORKDIR "/app"

RUN apt-get update
RUN apt-get install -y libzip-dev zip
RUN docker-php-ext-install zip pdo pdo_mysql mysqli
RUN pecl install -o -f redis && docker-php-ext-enable redis
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
