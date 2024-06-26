FROM --platform=$BUILDPLATFORM php:8.3-fpm-alpine3.19

RUN \
    # deps
    apk add -U --no-cache --virtual temp \
    # dev deps
    autoconf g++ file re2c make zlib-dev oniguruma-dev icu-data-full icu-dev bash\
    openldap-dev libzip-dev libmemcached-dev postgresql-dev \
    # prod deps
    && apk add --no-cache \
    zlib icu libpq libzip git linux-headers openldap openldap-back-mdb libmemcached \
    freetype-dev libpng-dev jpeg-dev libjpeg-turbo-dev shadow \
    # php extensions
    && docker-php-source extract \
    && pecl channel-update pecl.php.net \
    && { php -m | grep gd || docker-php-ext-configure gd --with-freetype --with-jpeg --enable-gd; } \
    && docker-php-ext-install bcmath gd intl pcntl ldap opcache pdo_mysql pdo_pgsql zip \
    && { pecl clear-cache || true; } \
    && pecl install memcached redis xdebug \
    && docker-php-source delete \
    #
    # composer
    && curl -sSL https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    #
    # cleanup
    && apk del temp \
    && rm -rf /var/cache/apk/* /tmp/* /var/tmp/* /usr/share/doc/* /usr/share/man/*

EXPOSE 9000

COPY src/usr/local/share/ca-certificates/rcert.pem /usr/local/share/ca-certificates/rcert.pem
COPY src/usr/local/share/ca-certificates/YandexInternalRootCA.crt /usr/local/share/ca-certificates/YandexInternalRootCA.crt
RUN update-ca-certificates

RUN echo "php_admin_flag[log_errors] = on" >> /usr/local/etc/php-fpm.d/www.conf

CMD ["php-fpm", "-y", "/usr/local/etc/php-fpm.conf", "-R"]