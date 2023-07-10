FROM php:7.2.34-fpm-buster
LABEL maintainer="haruu11113"
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

# timezone environment
ENV TZ=UTC \
    # locale
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    # composer environment
    COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer

COPY --from=composer:1.8.0 /usr/bin/composer /usr/bin/composer
COPY ./infra/docker/php/php-fpm.d/zzz-www.conf /usr/local/etc/php-fpm.d/zzz-www.conf
COPY ./infra/docker/php/php.ini /usr/local/etc/php/php.ini

RUN apt-get -y update \
    && apt-get -y install git vim libicu-dev libonig-dev libzip-dev unzip locales curl wget gnupg \
    && apt-get -y install autoconf gcc g++ libc-dev pkg-config re2c \
    && apt-get -y install zlib1g-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && locale-gen en_US.UTF-8 \
    && localedef -f UTF-8 -i en_US en_US.UTF-8 \
    && mkdir /var/run/php-fpm

WORKDIR /home/ec2-user/


# ## for php-mecab MeCabのインスtール
# RUN cd /tmp \
#     && wget "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7cENtOXlicTFaRUE" -O mecab-0.996.tar.gz \
#     && tar zxf mecab-0.996.tar.gz \
#     && cd mecab-0.996 \
#     && ./configure --enable-utf8-only --with-charset=utf8 \
#     && make \ && make install

# ## for php-mecab 辞書
# RUN cd /tmp \
#     && wget "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7MWVlSDBCSXZMTXM" -O mecab-ipadic-2.7.0-20070801.tar.gz \
#     && tar zxf mecab-ipadic-2.7.0-20070801.tar.gz \
#     && cd mecab-ipadic-2.7.0-20070801 \
#     && ./configure --with-charset=utf8 \
#     && make \
#     && make install

# ## for php-mecab
# RUN COPY ./infra/docker/php/php.mecab.ini /usr/local/etc/php/conf.d/ \
#     && git clone https://github.com/rsky/php-mecab.git \
#     && cd ./php-mecab/mecab \
#     && phpize \
#     && ./configure --with-php-config=/usr/local/bin/php-config --with-mecab=/usr/local/bin/mecab-config \
#     && make \
#     && make test \ && make install
#     # && cd ../../ \
#     # && rm -rf php-mecab

RUN apt-get update -y \
    && apt-get -y install libjpeg-dev libpng-dev \
    && docker-php-ext-configure gd \
    && docker-php-ext-install gd intl pdo pdo_mysql zip bcmath \
    && composer config -g process-timeout 3600 \
    && composer config -g repos.packagist composer https://packagist.org


## for npm
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs \
    && npm install npm@latest -g


# ## for python
# RUN git clone https://github.com/pyenv/pyenv.git /home/ec2-user/.pyenv \
#     && cd /home/ec2-user/.pyenv \
#     && src/configure \
#     && make -C src
# COPY ./infra/.bashrc /home/ec2-user/.bashrc


# ## for R?
# RUN source /home/ec2-user/.bashrc \
#     && apt-get update \
#     && apt-get install -y build-essential libbz2-dev libdb-dev libreadline-dev libffi-dev \
#     && apt-get install -y libgdbm-dev liblzma-dev libncursesw5-dev libsqlite3-dev libssl-dev \
#     &&  apt-get install -y zlib1g-dev uuid-dev tk-dev zlib1g-dev libpng-dev \
#     && source /home/ec2-user/.bashrc \
#     && docker-php-ext-install -j$(nproc) gd

# RUN apt-get update \
#     && apt-get clean \
#     && pecl install grpc \
#     && pecl install protobuf \
#     && apt-get install -y r-base

WORKDIR /home/ec2-user/code/ea/
