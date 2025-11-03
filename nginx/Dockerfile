FROM php:8.2-fpm


# Cài extension cần cho Laravel
RUN docker-php-ext-install pdo pdo_mysql

# --- Install các extension cần thiết cho Laravel ---
RUN apt-get update && apt-get install -y \
    git curl zip unzip libpng-dev libonig-dev libxml2-dev libzip-dev \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

RUN docker-php-ext-install -j$(nproc) pdo_mysql mbstring exif pcntl bcmath gd zip

# --- Cài Composer ---
COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

# --- Set thư mục làm việc ---
WORKDIR /var/www


# --- Phân quyền cho storage và bootstrap ---
#RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache

# --- Mở port (optional) ---
EXPOSE 9000

# --- Chạy PHP-FPM ---
CMD ["php-fpm"]
