FROM php:7.3.33-fpm

 COPY php.ini /usr/local/etc/php/conf.d/zzz.ini

 # Update the package lists and install Git
RUN apt-get update \
    && apt-get install -y git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# RUN chmod +x /usr/local/bin/install-php-extensions && \
#      install-php-extensions intl gd pdo_mysql


## INFO : NEW GD WITH FREETYPE FOR PHP 7.4+ only
# # Install system dependencies
#  RUN apt-get update && \
#      apt-get install -y libpng-dev libjpeg-dev libfreetype6-dev libwebp-dev

# # Install GD extension
#  RUN docker-php-ext-configure gd --with-jpeg --with-freetype --with-webp \
#      && docker-php-ext-install -j$(nproc) gd


  #Install system dependencies
  RUN apt-get update && \
      apt-get install -y libpng-dev libjpeg-dev libfreetype6-dev libmagickwand-dev imagemagick 

   #Install GD extension (did seem to work with jpeg for some rease)
  #RUN docker-php-ext-install gd

# 
# Compile and install GD extension with JPEG support
RUN docker-php-source extract && \
    cd /usr/src/php/ext/gd && \
    phpize && \
    ./configure --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    make && \
    make install && \
    docker-php-source delete

# Enable GD extension
RUN docker-php-ext-enable gd
  

   #Install system dependencies
  RUN apt-get update && \
      apt-get install -y libicu-dev

  #Install intl extension
  RUN docker-php-ext-install intl

   #Install system dependencies
  RUN apt-get update && \
      apt-get install -y libonig-dev libzip-dev

   #Install pdo_mysql extension
  RUN docker-php-ext-install pdo_mysql

  








# RUN apt-get -y update
# RUN apt-get -y install git
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







