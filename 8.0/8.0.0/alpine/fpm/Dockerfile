FROM php:8.0.0-fpm-alpine3.12

LABEL maintainer="lee1031 <ligangmingx@gmail.com>"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update \
    && apk upgrade \
    && apk --update --virtual build-deps add \
        autoconf \
        make \
        gcc \
        g++ \
        libtool \
        pcre-dev \
        openssl-dev \
        freetype-dev libjpeg-turbo-dev libpng-dev \
        imap-dev \
        icu-dev \
        libxml2-dev \
        libzip-dev \
        bzip2-dev \
        gettext-dev \
        postgresql-dev \
        libxslt-dev \
        imagemagick-libs \
        imagemagick-dev \
        libmemcached-dev \
        openldap-dev \
        gmp-dev \
        file git automake libtool gettext gettext-dev g++ texinfo curl \
    && apk add --no-cache \
        tzdata freetype libjpeg-turbo libpng \
        imagemagick \
        libmemcached \
        libpq \
        libxslt \
        libzip \
        c-client \
        icu \
        supervisor \
        inotify-tools \
    && git clone --recursive --depth=1 -b 1.15.0 https://github.com/emcrisostomo/fswatch.git \
    && cd fswatch \
    && ./autogen.sh && ./configure && make -j && make install \
    && cd .. && rm -rf fswatch \
    && git clone --recursive --depth=1 https://github.com/Imagick/imagick \
    && cd imagick \
    && phpize && ./configure \
    && make \
    && make install \
    && docker-php-ext-enable imagick \
    && cd .. && rm -rf imagick \
    && docker-php-ext-configure gd \
           --with-freetype \
           --with-jpeg \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure ldap --with-libdir=lib/ \
    && docker-php-ext-install -j$(nproc) \
        pcntl \
        ldap \
        zip \
        gd \
        imap \
        intl \
        bcmath \
        bz2 \
        calendar \
        exif \
        gettext \
        mysqli \
        opcache \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        soap \
        sockets \
        gmp \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && yes '' | pecl install memcached && docker-php-ext-enable memcached \
    && pecl install mongodb && docker-php-ext-enable mongodb \
    && yes '' | pecl install redis && docker-php-ext-enable redis \
    && yes '' | pecl install apcu && docker-php-ext-enable apcu \
    && pecl install swoole && docker-php-ext-enable swoole \
    && docker-php-source delete \
    && apk \
    del build-deps \
    && rm -rf /var/cache/apk/* /var/lib/apk/* /etc/apk/cache/* \
    && rm -rf /tmp/* /var/tmp/*
