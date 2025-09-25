# backend/Dockerfile
FROM php:8.2-fpm

# system deps
RUN apt-get update && apt-get install -y \
    git unzip libpq-dev libzip-dev zip \
    libonig-dev libxml2-dev \
    && docker-php-ext-install pdo_pgsql mbstring xml

# composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

# copy app
COPY . .

# install deps
RUN composer install --no-dev --no-interaction --prefer-dist --optimize-autoloader

# permissions
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

EXPOSE 9000
CMD ["php-fpm"]
