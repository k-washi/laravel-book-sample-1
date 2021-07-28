FROM php:8.0-fpm-buster
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ENV COMPOSER_ALLOW_SUPERUSER 1

RUN apt-get update \
    # apt-get install
    && apt-get install -y --no-install-recommends \
    unzip git vim \
    libzip-dev libicu-dev libpq-dev \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    # docker-php-ext-install
    && docker-php-ext-install \
    gd intl zip \
    pdo_pgsql pgsql  \
    # clear cache
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# configure modules
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-configure gd --with-freetype --with-jpeg

# php.conf php-fpm.conf
COPY conf/php.ini /usr/local/etc/php/php.ini
COPY conf/docker.conf /usr/local/etc/php-fpm.d/docker.conf

# install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

RUN composer config -g process-timeout 3600 && \
    composer config -g repos.packagist composer https://packagist.org

WORKDIR /app