FROM php:7.1-fpm

RUN curl -s https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN curl -sL https://deb.nodesource.com/setup_8.x  | bash - \
    && apt-get install -y nodejs

RUN apt-get update \
    && apt-get install -y postgresql-client-9.5 libjpeg62-turbo-dev libpng12-dev  \
        libbz2-dev libfreetype6-dev libpq-dev libicu-dev unzip git wget alien  libaio1 libaio-dev cron gdal-bin

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include --with-jpeg-dir=/usr/include \
  && docker-php-ext-install -j$(nproc) \
          gd \
          pdo_pgsql \
          pdo_mysql \
          zip \
          bcmath \
          bz2 \
          gettext \
          intl \
          sockets \
          && pecl install apcu \
          && docker-php-ext-enable \
          apcu


RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php -r "copy('https://composer.github.io/installer.sig', 'composer-setup.sig');" \
 && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('composer-setup.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
 && php composer-setup.php \
 && php -r "unlink('composer-setup.php');" \
 && mv composer.phar /usr/local/bin/composer
