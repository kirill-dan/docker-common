FROM ubuntu:18.04

# Import variables from docker-compose file
ARG PROJECT_NAME
ARG PROJECT_DOMEN

RUN apt-get update && apt-get install -y software-properties-common
#RUN add-apt-repository ppa:ondrej/php && apt-get update

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
	php7.2 \
	php7.2-cli \
	php7.2-fpm \
	php7.2-opcache \
	php7.2-zip \
	php7.2-xmlrpc \
	php7.2-xsl \
	php7.2-mbstring \
	php7.2-mysql \
	php7.2-mysqli \
	php7.2-odbc \
	php7.2-pgsql \
	php7.2-pspell \
	php7.2-readline \
	php7.2-recode \
	php7.2-snmp \
	php7.2-soap \
	php7.2-sqlite3 \
	php7.2-sybase \
	php7.2-tidy \
	php7.2-xml \
	php7.2-json \
	php7.2-ldap \
	php7.2-intl \
	php7.2-interbase \
	php7.2-imap \
	php7.2-gmp \
	php7.2-gd \
	php7.2-enchant \
	php7.2-dba \
	php7.2-bz2 \
	php7.2-bcmath \
	php7.2-phpdbg \
	php7.2-cgi \
	php7.2-cli \
	php7.2-xdebug \
	php7.2-redis \
	php7.2-curl \
	php7.2-imagick

RUN service php7.2-fpm start

RUN mkdir -p /usr/local/bin
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN touch /etc/php/7.2/fpm/conf.d/$PROJECT_NAME
RUN echo "date.timezone = UTC" >> /etc/php/7.2/fpm/conf.d/$PROJECT_NAME
RUN echo "date.timezone = UTC" >> /etc/php/7.2/cli/conf.d/$PROJECT_NAME

ADD settings.pool.conf /etc/php/7.2/fpm/pool.d/
RUN mv /etc/php/7.2/fpm/pool.d/settings.pool.conf /etc/php/7.2/fpm/pool.d/${PROJECT_NAME}.pool.conf

RUN sed -i 's/{PROJECT_NAME}/'$PROJECT_NAME'/g' /etc/php/7.2/fpm/pool.d/${PROJECT_NAME}.pool.conf
RUN sed -i 's/{PROJECT_DOMEN}/'$PROJECT_NAME'/g' /etc/php/7.2/fpm/pool.d/${PROJECT_NAME}.pool.conf

RUN usermod -u 1000 www-data

CMD ["php7.2-fpm", "-F"]

EXPOSE 9001
