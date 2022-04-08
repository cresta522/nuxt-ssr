
FROM php:8.0-fpm
# timezone
ARG TZ

COPY ./docker/php/php.ini /usr/local/etc/php/
COPY ./laravel/ /var/www/laravel/

# Composer install
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

ARG GID
ARG UID
ARG GROUPNAME
ARG USERNAME

RUN groupadd -g $GID $GROUPNAME
RUN useradd -m -s /bin/bash -u $UID -g $GID -G sudo $USERNAME
RUN echo $USERNAME:passwd | chpasswd
USER $USERNAME

# install packages including Node.js
RUN apt-get update && \
    curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && \
    apt-get -y install \
    nodejs\
    git \
    zip \
    unzip \
    vim \
    cron \
    procps \
    && docker-php-ext-install pdo_mysql bcmath

# cron
RUN service cron start
RUN echo '* * * * * root cd /app && php artisan schedule:run >> /dev/null 2>&1' >> /etc/crontab

RUN chmod -R 777 /var/www/laravel

WORKDIR /var/www/laravel
