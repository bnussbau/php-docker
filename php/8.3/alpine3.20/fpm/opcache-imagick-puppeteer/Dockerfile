FROM php:8.3-fpm-alpine3.20

# Install system dependencies
RUN apk add --no-cache \
    nginx \
    supervisor \
    libpq \
    nodejs \
    npm \
    git \
    curl \
    zip \
    unzip \
    imagemagick-dev \
    chromium

# Configure Chromium Path
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium
ENV PUPPETEER_DOCKER=1

RUN mkdir -p /usr/src/php/ext/imagick
RUN chmod 777 /usr/src/php/ext/imagick
RUN curl -fsSL https://github.com/Imagick/imagick/archive/refs/tags/3.7.0.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1

# Install PHP extensions
RUN docker-php-ext-install opcache imagick
