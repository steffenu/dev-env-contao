FROM php:8.2-fpm

COPY php.ini /usr/local/etc/php/conf.d/zzz.ini

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
     install-php-extensions intl gd pdo_mysql

# Install necessary PHP extensions
# RUN apt-get update \
#     && apt-get install -y \
#         libicu-dev \
#         libzip-dev \
#         zlib1g-dev \
#         libpng-dev \
#         libjpeg-dev \
#         libfreetype6-dev \
#     && docker-php-ext-install -j$(nproc) \
#         intl \
#         pdo_mysql \
#         zip \
#         gd  

WORKDIR /var/www   
RUN rm -rf html

# INSTALL EXTENSION FOR CONTAO 5
# Note : The Image already contains some Extensions
# Extension Requirements taken from 
# https://github.com/contao/contao/blob/5.x/composer.json
# https://docs.contao.org/manual/de/installation/systemvoraussetzungen/



# sudo apt -y install php8.1-cli php8.1-mysql php8.1-sqlite3 php8.1-intl php8.1-mbstring php8.1-curl php8.1-xml php8.1-gd php8.1-zip php8.1-dom php8.1-pdo

# gd
#

  # "ext-dom": "*", XX 
  # "ext-pcre": "*", XX
  # "ext-intl": "*", ADDED
  # "ext-pdo": "*", XX
  # "ext-zlib": "*", XX
  # "ext-json": "*", XX
  # "ext-curl": "*", XX
  # "ext-mbstring": "*", XX
  # "ext-gd": "*", XX
  # "ext-filter": "*", XX
  # "ext-hash": "*", XX
  # "ext-fileinfo": "*", XX
  # "ext-session": "*", XX

# OPTIONAL
  # "ext-imagick": "*",
  # "ext-gmagick": "*",







