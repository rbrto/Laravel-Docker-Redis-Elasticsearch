FROM php:7.1-fpm

# Instalando extensiones PHP
RUN apt-get update && apt-get install -y \
      libicu-dev \
      libpq-dev \
      libmcrypt-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-install \
      intl \
      mbstring \
      mcrypt \
      pcntl \
      pdo_mysql \
      pdo_pgsql \
      pgsql \
      zip \
      opcache

# Instalando composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# Instalando phpunit
RUN curl https://phar.phpunit.de/phpunit.phar -L > phpunit.phar \
  && chmod +x phpunit.phar \
  && mv phpunit.phar /usr/local/bin/phpunit \
  && phpunit --version

# Instalando cron
RUN apt-get update && apt-get -y install rsyslog

# Cambiando uid y gid de apache al usuario docker uid/gid
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# Estableciendo el directorio raiz dentro del contenedor
WORKDIR /var/www/html
