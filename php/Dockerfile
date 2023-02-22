FROM php:8.1-apache

FROM php:8.1-apache
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN a2enmod userdir
RUN a2enmod rewrite
ADD userdir.conf /etc/apache2/mods-enabled/

RUN apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/src/php/ext/imagick; \
    curl -fsSL https://github.com/Imagick/imagick/archive/06116aa24b76edaf6b1693198f79e6c295eda8a9.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1; \
    docker-php-ext-install imagick;



