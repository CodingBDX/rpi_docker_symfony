FROM php:8.1-apache

RUN apt-get update \
    &&  apt-get install -y --no-install-recommends \
        locales apt-utils zsh git libicu-dev  g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev unzip libpq-dev nodejs  npm wget \
        apt-transport-https lsb-release ca-certificates

RUN apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/src/php/ext/imagick; \
    curl -fsSL https://github.com/Imagick/imagick/archive/06116aa24b76edaf6b1693198f79e6c295eda8a9.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1; \
    docker-php-ext-install imagick;

RUN curl -sS https://getcomposer.org/installer | php -- \
    &&  mv composer.phar /usr/local/bin/composer

RUN curl -sS https://get.symfony.com/cli/installer | bash \
    &&  mv /root/.symfony5/bin/symfony /usr/local/bin/symfony




RUN docker-php-ext-configure \
            intl \
    &&  docker-php-ext-install \
 mysqli pdo pdo_mysql pdo_pgsql opcache intl zip calendar dom mbstring gd xsl
RUN a2enmod userdir
RUN a2enmod rewrite
ADD userdir.conf /etc/apache2/mods-enabled/



RUN pecl install apcu && docker-php-ext-enable apcu


RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash


RUN npm install --global yarn

RUN git config --global user.email "antonycharier@gmail.com" \
    &&  git config --global user.name "CodingBDX"

