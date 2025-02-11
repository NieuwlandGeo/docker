FROM cimg/php:8.4.3-browsers

USER root

RUN apt-get update

RUN apt-get install -y gdal-bin libmagickwand-dev

ADD php.ini /etc/php.d/

RUN mkdir /app \
    && mkdir /var/jwt \
    && chown -R circleci /app \
    && chown -R circleci /var/jwt

USER circleci

RUN openssl genrsa -out /var/jwt/private_test.pem -aes256 -passout pass:wgp5foo 4096
RUN openssl rsa -passin pass:wgp5foo -pubout -in /var/jwt/private_test.pem -out /var/jwt/public_test.pem
