# Use PHP 8.2 with Apache
FROM php:8.2-apache

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libicu-dev \
    libpq-dev \
    zip \
    && docker-php-ext-install \
    pdo_pgsql \
    intl \
    opcache

# Enable Apache modules
RUN a2enmod rewrite

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Create necessary directories and set permissions
RUN mkdir -p \
    /var/www/.composer \
    /var/www/html/vendor \
    /var/www/html/var \
    && chown -R www-data:www-data /var/www

# Set proper permissions for the Apache user
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# Copy composer files
COPY composer.* ./

# Set proper ownership
RUN chown -R www-data:www-data .

# Switch to www-data user
USER www-data

# Install dependencies
RUN composer install --no-scripts --no-autoloader

# Copy source code
COPY --chown=www-data:www-data . .

# Generate optimized autoloader
RUN composer dump-autoload --optimize

# Switch back to root for Apache
USER root

# Apache configuration
COPY docker/apache.conf /etc/apache2/sites-available/000-default.conf

# Expose port
EXPOSE 80