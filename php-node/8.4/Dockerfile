FROM php:8.4-fpm-bookworm

RUN apt-get update \
  && apt-get install -y gnupg

RUN curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|gpg --dearmor -o /usr/share/keyrings/postgresql-archive-keyring.gpg \
  && echo "deb [signed-by=/usr/share/keyrings/postgresql-archive-keyring.gpg] https://apt.postgresql.org/pub/repos/apt/ bookworm-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN apt-get update \
  && apt-get install -y postgresql-client-17 libjpeg62-turbo-dev libpng-dev libzip-dev \
  libbz2-dev libfreetype6-dev libpq-dev libicu-dev unzip git wget gdal-bin \
  libmagickwand-dev

RUN curl -fsSL https://packages.redis.io/gpg | gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg \
  && echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb bookworm main" > /etc/apt/sources.list.d/redis.list

RUN apt-get update \
  && apt-get install -y redis

RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - \
  && apt-get install -y nodejs

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
  && docker-php-ext-enable apcu

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "copy('https://composer.github.io/installer.sig', 'composer-setup.sig');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('composer-setup.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && php -r "unlink('composer-setup.php');"
