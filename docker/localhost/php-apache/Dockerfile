FROM php:7.2-apache

# put config
COPY ./php.ini /usr/local/etc/php/

# setup php
RUN apt-get update && apt-get install -y \
  gcc \
  make \
  vim \
  wget \
  zip \
  unzip \
  iputils-ping \
  git \
  curl \
  default-mysql-client \
  libxml2-dev  \
  libsodium-dev \
  openssl \
  libpng-dev \
  gnupg \
  libjpeg-dev \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libmagickwand-dev \
  libzip-dev \
  libmcrypt-dev \
  libmemcached-dev \
  zlib1g-dev

# install php extension
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install dom
RUN docker-php-ext-install exif
RUN docker-php-ext-install fileinfo
RUN docker-php-ext-install hash
RUN docker-php-ext-install json
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mysqli \
  && docker-php-ext-enable mysqli
RUN docker-php-ext-install sodium
RUN docker-php-ext-install xml
RUN docker-php-ext-install zip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install iconv
RUN docker-php-ext-install simplexml
RUN pecl install imagick
RUN docker-php-ext-enable imagick
RUN pecl install memcached-3.1.4
RUN docker-php-ext-enable memcached opcache

# Xdiff install
RUN curl -L -o /tmp/xdiff.tar.gz 'http://www.xmailserver.org/libxdiff-0.23.tar.gz' \
  && mkdir -p /usr/src/xdiff \
  && tar -C /usr/src/xdiff -zxvf /tmp/xdiff.tar.gz --strip 1 \
  && rm /tmp/xdiff.tar.gz \
  && cd /usr/src/xdiff \
  && ./configure  && make && make install \
  \
  &&  pecl install xdiff-2.0.1 && docker-php-ext-enable xdiff

RUN a2enmod rewrite
RUN a2enmod headers
RUN a2enmod include
RUN ln -s /etc/apache2/mods-available/vhost_alias.load /etc/apache2/mods-enabled
RUN echo ServerName $HOSTNAME > /etc/apache2/conf-available/fqdn.conf && a2enconf fqdn

COPY ./localhost.conf /etc/apache2/sites-available
RUN a2ensite localhost.conf
RUN a2dissite 000-default

EXPOSE 80
