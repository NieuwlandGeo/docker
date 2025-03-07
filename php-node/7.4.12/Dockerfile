FROM php:7.4-fpm-buster

RUN apt-get update \
  && apt-get install -y gnupg

RUN curl -s https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && echo "deb https://apt-archive.postgresql.org/pub/repos/apt bionic-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - \
  && apt-get install -y nodejs

RUN apt-get update \
  && apt-get install -y postgresql-client-9.6 libjpeg62-turbo-dev libpng-dev libzip-dev \
  libbz2-dev libfreetype6-dev libpq-dev libicu-dev unzip git wget gdal-bin \
  libmagickwand-dev

RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) \
  gd \
  pdo_pgsql \
  zip \
  bcmath \
  bz2 \
  gettext \
  intl \
  sockets \
  && pecl install apcu \
  && docker-php-ext-enable apcu \
  && pecl install imagick \
  && docker-php-ext-enable imagick \
  && pecl install redis-4.0.2 \
  && docker-php-ext-enable redis

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "copy('https://composer.github.io/installer.sig', 'composer-setup.sig');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('composer-setup.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && php -r "unlink('composer-setup.php');" 

