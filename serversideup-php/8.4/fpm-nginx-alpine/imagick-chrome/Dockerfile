FROM serversideup/php:8.4-fpm-nginx-alpine AS laravel

USER root
# Install system dependencies
RUN apk add --no-cache \
    npm \
    git \
    curl \
    zip \
    unzip \
    imagemagick-dev \
    chromium && \
    mkdir -p /usr/src/php/ext/imagick && \
    chmod 777 /usr/src/php/ext/imagick && \
    curl -fsSL https://github.com/Imagick/imagick/archive/refs/tags/3.8.0.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1

# Environment
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium
ENV PUPPETEER_DOCKER=1

# Install PHP extensions
RUN install-php-extensions imagick

USER www-data

WORKDIR /var/www/html

COPY --chown=www-data:www-data ./etc/s6-overlay/s6-rc.d/laravel-queue /etc/s6-overlay/s6-rc.d/laravel-queue
COPY --chown=www-data:www-data ./etc/s6-overlay/s6-rc.d/laravel-scheduler /etc/s6-overlay/s6-rc.d/laravel-scheduler
COPY --chown=www-data:www-data ./etc/s6-overlay/s6-rc.d/user/contents.d /etc/s6-overlay/s6-rc.d/user/contents.d

# Standardport für Nginx und PHP-FPM
EXPOSE 8080