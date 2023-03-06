FROM cimg/php:8.1.16-browsers

USER root

RUN apt-get update

RUN apt-get install -y gdal-bin libmagickwand-dev

RUN pecl install imagick

RUN cd /tmp \
    && sudo wget "https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz" \
    && sudo tar xvf /tmp/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
    && sudo mv /tmp/wkhtmltox/bin/* /usr/local/bin \
    && sudo mv /tmp/wkhtmltox/include/* /usr/local/include \
    && sudo mv /tmp/wkhtmltox/lib/* /usr/local/lib \
    && sudo mkdir -p /usr/local/share/man/man1 \
    && sudo mv /tmp/wkhtmltox/share/man/man1/* /usr/local/share/man/man1 \
    && sudo rm -rf /usr/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
    && sudo rm -rf /usr/wkhtmltox

ADD php.ini /usr/local/etc/php/

RUN mkdir /app \
    && mkdir /var/jwt \
    && chown -R circleci /app \
    && chown -R circleci /var/jwt

USER circleci

RUN openssl genrsa -out /var/jwt/private_test.pem -aes256 -passout pass:wgp5foo 4096
RUN openssl rsa -passin pass:wgp5foo -pubout -in /var/jwt/private_test.pem -out /var/jwt/public_test.pem
