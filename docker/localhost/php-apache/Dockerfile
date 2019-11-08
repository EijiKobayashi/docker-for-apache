FROM php:7.2-apache

COPY ./php.ini /usr/local/etc/php/

RUN apt-get update \
  && apt-get install -y \
  gcc \
  make \
  git \
  unzip \
  vim \
  wget \
  default-mysql-client \
  zlib1g-dev \
  libmcrypt-dev \
  curl \
  gnupg \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  libjpeg-dev \
  && docker-php-ext-install pdo_mysql mysqli zip \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd

RUN a2enmod rewrite
RUN a2enmod headers
RUN a2enmod include
RUN ln -s /etc/apache2/mods-available/vhost_alias.load /etc/apache2/mods-enabled
RUN echo ServerName $HOSTNAME > /etc/apache2/conf-available/fqdn.conf && a2enconf fqdn

COPY ./localhost.conf /etc/apache2/sites-available
RUN a2ensite localhost.conf
RUN a2dissite 000-default

EXPOSE 80
