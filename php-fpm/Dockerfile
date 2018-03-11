FROM ubuntu:17.10

# Import variables from docker-compose file
ARG PROJECT_NAME
ARG PROJECT_DOMEN

RUN apt-get update && apt-get install -y software-properties-common

RUN apt-get install -y locales locales-all
RUN sed -i -e 's/# ru_RU.UTF-8 UTF-8/ru_RU.UTF-8 UTF-8/' /etc/locale.gen && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen && \
    update-locale LANG=ru_RU.UTF-8 && \
    echo "LANGUAGE=ru_RU.UTF-8" >> /etc/default/locale && \
    echo "LC_ALL=ru_RU.UTF-8" >> /etc/default/locale

RUN apt-get install tzdata

RUN echo Europe/Kiev > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

WORKDIR /var/www/${PROJECT_DOMEN}/

RUN apt-get update && apt-get install -y \
	curl \
	git	\
	wget \
    mc \
	composer \
    zip \
    unzip \
	php7.1 \
	php7.1-fpm \
	php7.1-opcache \
	php7.1-zip \
	php7.1-xmlrpc \
	php7.1-xsl \
	php7.1-mbstring \
	php7.1-mcrypt \
	php7.1-mysql \
	php7.1-mysqli \
	php7.1-odbc \
	php7.1-pgsql \
	php7.1-pspell \
	php7.1-readline \
	php7.1-recode \
	php7.1-snmp \
	php7.1-soap \
	php7.1-sqlite3 \
	php7.1-sybase \
	php7.1-tidy \
	php7.1-xml \
	php7.1-json \
	php7.1-ldap \
	php7.1-intl \
	php7.1-interbase \
	php7.1-imap \
	php7.1-gmp \
	php7.1-gd \
	php7.1-enchant \
	php7.1-dba \
	php7.1-bz2 \
	php7.1-bcmath \
	php7.1-phpdbg \
	php7.1-cgi \
	php7.1-cli \
	php7.1-xdebug \
	php7.1-redis \
	php7.1-curl \
	php7.1-imagick

RUN service php7.1-fpm start

RUN mkdir -p /usr/local/bin
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN touch /etc/php/7.1/fpm/conf.d/$PROJECT_NAME
RUN echo "date.timezone = UTC" >> /etc/php/7.1/fpm/conf.d/$PROJECT_NAME
RUN echo "date.timezone = UTC" >> /etc/php/7.1/cli/conf.d/$PROJECT_NAME

ADD settings.pool.conf /etc/php/7.1/fpm/pool.d/
RUN mv /etc/php/7.1/fpm/pool.d/settings.pool.conf /etc/php/7.1/fpm/pool.d/${PROJECT_NAME}.pool.conf

RUN sed -i 's/{PROJECT_NAME}/'$PROJECT_NAME'/g' /etc/php/7.1/fpm/pool.d/${PROJECT_NAME}.pool.conf
RUN sed -i 's/{PROJECT_DOMEN}/'$PROJECT_NAME'/g' /etc/php/7.1/fpm/pool.d/${PROJECT_NAME}.pool.conf

RUN usermod -u 1000 www-data

CMD ["php7.1-fpm", "-F"]

EXPOSE 9001
