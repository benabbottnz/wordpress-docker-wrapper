FROM php:8.0-apache

RUN apt-get update \
    # Database.
    && docker-php-ext-install mysqli \
    # Zip.
    && apt-get install -y libzip-dev \
    && docker-php-ext-install zip \
    # GD.
    && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libwebp-dev \
    && docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install -j$(nproc) gd \
    # Imagick.
    && apt-get install -y imagemagick libmagickwand-dev \
    && pecl install -o -f imagick \
    && docker-php-ext-enable imagick \
    # Exif.
    && docker-php-ext-install exif \
    # Cleanup.
    && rm -rf /var/lib/apt/lists/*

# Custom ini settings.
COPY conf.d/custom.ini /usr/local/etc/php/conf.d/custom.ini

RUN a2enmod rewrite
RUN a2enmod expires
RUN a2enmod headers
