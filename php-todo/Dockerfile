# FROM php:7.4-fpm-alpine
FROM php:7-apache
LABEL maintainer="Nnaemeka Okpallannuozo"

WORKDIR /var/www/html

#install zip, unzip extension, git
RUN apt-get update && apt-get install -y \
  git \
  zip \
  unzip

RUN docker-php-ext-install pdo_mysql mysqli

COPY apache-config.conf /etc/apache2/sites-available/000-default.conf
COPY start-apache /usr/local/bin
RUN a2enmod rewrite

COPY . ./

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD .env.sample ./.env

RUN chmod -R 755 ./storage

RUN chown -R www-data:www-data /var/www

RUN chmod +x ./start-apache

EXPOSE 80

CMD ["start-apache"]
