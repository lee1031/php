# Alpine PHP-FPM Docker Image

Docker container to install and run [PHP-FPM](https://www.php.net/).

[![Build Status](https://travis-ci.org/lee1031/php.svg?branch=master)](https://travis-ci.org/lee1031/php)
[![Docker Automated build](https://img.shields.io/docker/automated/jrottenberg/ffmpeg.svg)](https://hub.docker.com/r/lee1031/php)

## Supported branches 
- 7.4: `7.4.8-fpm`、`7.4.7-fpm`、`7.4.6-fpm`、`7.4.5-fpm`
- 7.3: `7.3.20-fpm`、`7.3.19-fpm`、`7.3.18-fpm`、`7.3.17-fpm`




## Getting image

```sh
docker pull lee1031/php
```

## Running your PHP script

```sh
sudo docker container run --rm -v $(pwd):/var/www/html lee1031/php php index.php
```

## Running as server

```sh
sudo docker container run --rm --name php-fpm -v $(pwd):/var/www/html -p 8080:8080 lee1031/php php -S="0.0.0.0:8080" -t="/var/www/html"
```

## using  [Docker Compose](https://docs.docker.com/compose/)

```sh
version: '3'
services:
  php-fpm:
    container_name: php-fpm
    image: lee1031/php
    ports:
      - 8080:8080
    volumes:
      - ./:/var/www/html
    command: php -S="0.0.0.0:8080" -t="/var/www/html"
```

```sh
version: '3'
services:
    php-fpm:
        image: lee1031/php:7.3.9-fpm
        ports:
            - "9000:9000"
        restart: always
        volumes:
            - "./:/var/www/html:rw"
        command:
            - /bin/sh
            - -c
            - |
                cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini
                php-fpm
        environment:
            TZ: "Asia/Shanghai"
```


### [PHP Modules]
- apcu
- bcmath
- bz2
- calendar
- Core
- ctype
- curl
- date
- dom
- exif
- fileinfo
- filter
- ftp
- gd
- gettext
- gmp
- hash
- iconv
- imagick
- imap
- inotify
- intl
- json
- ldap
- libxml
- mbstring
- memcached
- mongodb
- mysqli
- mysqlnd
- openssl
- pcntl
- pcre
- PDO
- pdo_mysql
- pdo_pgsql
- pdo_sqlite
- pgsql
- Phar
- posix
- readline
- redis
- Reflection
- session
- SimpleXML
- soap
- sockets
- sodium
- SPL
- sqlite3
- standard
- swoole
- tokenizer
- xdebug
- xml
- xmlreader
- xmlrpc
- xmlwriter
- xsl
- Zend OPcache
- zip
- zlib

### [Zend Modules]
- Xdebug
- Zend OPcache
