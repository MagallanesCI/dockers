# docker build ./ -t magallanesci/php:7.4 --no-cache
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive \
    TZ=UTC

# Packages
RUN echo 'APT::Acquire::Retries "3";' > /etc/apt/apt.conf.d/80-retries
RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends locales ca-certificates curl git unzip software-properties-common gpg-agent
RUN add-apt-repository -y ppa:ondrej/php && apt-get update -y

# apt-cache search php7.4 | grep "^php7.4" | cut -d' ' -f1 | sort
RUN apt-get install -y --no-install-recommends php7.4-amqp php7.4-bcmath php7.4-bz2 php7.4-cli php7.4-common \
    php7.4-curl php7.4-gd php7.4-gearman php7.4-gmp php7.4-gnupg php7.4-imagick php7.4-imap \
    php7.4-intl php7.4-mailparse php7.4-mbstring php7.4-memcache php7.4-memcached \
    php7.4-mongodb php7.4-msgpack php7.4-mysql php7.4-oauth php7.4-odbc php7.4-pcov php7.4-pgsql \
    php7.4-psr php7.4-readline php7.4-redis php7.4-snmp php7.4-soap php7.4-sqlite3 php7.4-ssh2 php7.4-uuid \
    php7.4-xdebug php7.4-xml php7.4-xmlrpc php7.4-xsl php7.4-yaml php7.4-zip php7.4-zmq
RUN apt-get dist-upgrade -y && apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/*

ADD conf.d/ /etc/php/7.4/cli/conf.d/
RUN mkdir /run/php/

# Composer v2
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer2
RUN composer2 self-update --2

# Composer v1
RUN cp -p /usr/bin/composer2 /usr/bin/composer1
RUN composer1 self-update --1

# Make Composer 2 the default
RUN ln -s /usr/bin/composer2 /usr/bin/composer
