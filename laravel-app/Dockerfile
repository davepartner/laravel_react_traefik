# Use an official PHP image with Apache
FROM php:8.2-apache

# Install system dependencies (for Laravel)
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    git \
    && docker-php-ext-install pdo_mysql

# Install Composer (PHP package manager)
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set working directory
WORKDIR /var/www/html

# Copy Laravel files (we’ll install it next)
COPY . .

# Install Laravel dependencies
RUN composer install --no-scripts --no-interaction

# Set permissions for Laravel
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Enable Apache rewrite module (for Laravel routing)
RUN a2enmod rewrite

# Expose port 80 (Apache default)
EXPOSE 80