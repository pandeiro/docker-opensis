FROM debian:jessie
MAINTAINER Murphy McMahon <pandeiro.docker@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update

# Dependencies

RUN apt-get -y install \
    supervisor \
    apache2 \
    libapache2-mod-php5 \
    mysql-server \
    php5-mysql \
    pwgen \
    php-apc \
    php5-mcrypt \
    wget

# Scripts

ADD bin/start-apache2           /start-apache2
ADD bin/start-mysql             /start-mysqld
ADD bin/create-mysql-admin-user /create-mysql-admin-user
ADD bin/init                    /init

# Configuration

ADD conf/my.cnf           /etc/mysql/conf.d/my.cnf
ADD conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf   

# Data

VOLUME  ["/etc/mysql", "/var/lib/mysql" ]

# Environment

ENV PHP_UPLOAD_MAX_FILESIZE 10M
ENV PHP_POST_MAX_SIZE 10M

# Ports

EXPOSE 80 3306

# Application Installation

RUN wget --quiet -O opensis-ml.tar.gz https://github.com/OS4ED/opensis-ml/archive/5.3.tar.gz \
    && tar xzvf opensis-ml.tar.gz \
    && rm -rf /var/www/html && ln -s /opensis-ml-5.3 /var/www/html

# Init

ENTRYPOINT ["/init"]
