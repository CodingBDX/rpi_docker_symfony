FROM php:8.1-apache

RUN apt-get update \
    &&  apt-get install -y --no-install-recommends \
        locales apt-utils zsh git libicu-dev  g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev unzip libpq-dev nodejs  npm wget \
        apt-transport-https lsb-release ca-certificates

RUN apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/src/php/ext/imagick; \
    curl -fsSL https://github.com/Imagick/imagick/archive/06116aa24b76edaf6b1693198f79e6c295eda8a9.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1; \
    docker-php-ext-install imagick;
# Uses "Spaceship" theme with some customization. Uses some bundled plugins and installs some more from github
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.2/zsh-in-docker.sh)" -- \
    -t https://github.com/denysdovhan/spaceship-prompt \
    -a 'SPACESHIP_PROMPT_ADD_NEWLINE="false"' \
    -a 'SPACESHIP_PROMPT_SEPARATE_LINE="false"' \
    -p git \
    -p gitfast \
    -p symfony \
    -p ssh-agent \
    -p https://github.com/zsh-users/zsh-autosuggestions \
    -p https://github.com/zsh-users/zsh-completions \
    -p https://github.com/zsh-users/zsh-syntax-highlighting



ENV APP_USER=zsh-user
ENV APP_USER_GROUP=www-data
ARG APP_USER_HOME=/home/$APP_USER

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen  \
    &&  echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    &&  locale-gen

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

RUN pecl install xdebug 
RUN docker-php-ext-enable xdebug

RUN pecl install apcu && docker-php-ext-enable apcu


RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash


RUN npm install --global yarn

RUN git config --global user.email "antonycharier@gmail.com" \
    &&  git config --global user.name "CodingBDX"

CMD tail -f /dev/null

WORKDIR /var/www/html/
