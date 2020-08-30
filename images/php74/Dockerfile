FROM php:7.4-fpm

ARG USER_ID
ARG GROUP_ID

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get update && apt-get install -y \
        git \
        curl \
        wget \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev zlib1g-dev libicu-dev g++ libmagickwand-dev --no-install-recommends libxml2-dev; \
    docker-php-ext-configure intl; \
    docker-php-ext-install intl; \
    pecl install mcrypt-1.0.3; \
    docker-php-ext-install mbstring zip xml gd mcrypt pdo_mysql; \
    pecl install imagick; \
    docker-php-ext-enable imagick; \
    pecl install xdebug-2.8.1; \
    docker-php-ext-enable xdebug;

ADD ./php.ini /usr/local/etc/php/php.ini

RUN wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer --quiet


RUN usermod -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data

WORKDIR /var/www

USER "${USER_ID}:${GROUP_ID}"

CMD ["php-fpm"]