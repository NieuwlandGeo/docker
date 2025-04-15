FROM cimg/php:8.4.3-browsers

USER root

RUN apt-get update

RUN apt-get install -y gdal-bin libmagickwand-dev

RUN pecl install imagick \
    && docker-php-ext-enable imagick

RUN cd /tmp \
    && wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.0g-2ubuntu4_amd64.deb \
    && dpkg -i libssl1.1_1.1.0g-2ubuntu4_amd64.deb \
    && wget "https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz" \
    && tar xvf /tmp/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
    && mv /tmp/wkhtmltox/bin/* /usr/local/bin \
    && mv /tmp/wkhtmltox/include/* /usr/local/include \
    && mv /tmp/wkhtmltox/lib/* /usr/local/lib \
    && mkdir -p /usr/local/share/man/man1 \
    && mv /tmp/wkhtmltox/share/man/man1/* /usr/local/share/man/man1 \
    && rm -rf /usr/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
    && rm -rf /usr/wkhtmltox

ADD php.ini /etc/php.d/

RUN mkdir /app \
    && mkdir /var/jwt \
    && chown -R circleci /app \
    && chown -R circleci /var/jwt

USER circleci

RUN openssl genrsa -out /var/jwt/private_test.pem -aes256 -passout pass:wgp5foo 4096
RUN openssl rsa -passin pass:wgp5foo -pubout -in /var/jwt/private_test.pem -out /var/jwt/public_test.pem
