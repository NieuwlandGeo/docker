FROM centos:latest

RUN yum -y update
RUN yum -y install centos-release-scl.noarch
RUN yum -y install epel-release
RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -
RUN yum -y install nodejs gcc-c++ make
RUN yum -y install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm
RUN yum -y install rh-php71-php-gd rh-php71-php-fpm rh-php71-php-intl rh-php71-php-xml \
  rh-php71-php-pgsql rh-php71-php-opcache rh-php71-php-cli rh-php71-php beanstalkd gdal
