FROM ubuntu:21.04
MAINTAINER Yusuf Doğan <yusufdogan21@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt list --upgradable
RUN apt-get update

#Installing the Nginx Web Server
RUN apt-get install nginx -y
RUN apt-get install apt-utils -y
RUN apt-get install git -y
RUN apt-get install curl -y
RUN apt-get install nano -y
RUN apt-get install mysql-client -y
RUN apt-get install openssl -y
RUN apt-get update

RUN apt-get update && apt-get install -y \
    php7.4-fpm \
    php7.4-cli \
    php7.4-json \
    php7.4-curl \
    php7.4-gd \
    php7.4-ldap \
    php7.4-mbstring \
    php7.4-mysql \
    php7.4-soap \
    php7.4-sqlite3 \
    php7.4-xml \
    php7.4-zip \
    php7.4-intl

RUN apt-get clean && rm -rf /var/lib/apt/lists/*
# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Nginx config
RUN rm /etc/nginx/sites-enabled/default
ADD default.conf /etc/nginx/sites-available/default.conf
RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf
RUN sed -i "s/user  nginx;/user  www-data;/g" /etc/nginx/nginx.conf

# Expose ports.
EXPOSE 80
#EXPOSE 443
WORKDIR /var/www/tatooine

CMD service php7.4-fpm start && nginx -g "daemon off;"
