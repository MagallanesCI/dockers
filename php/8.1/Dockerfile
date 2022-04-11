# docker build ./ -t magallanesci/php:8.1 --no-cache
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive \
    TZ=UTC

# Packages
RUN echo 'APT::Acquire::Retries "3";' > /etc/apt/apt.conf.d/80-retries
RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends locales ca-certificates curl git unzip software-properties-common gpg-agent
RUN add-apt-repository -y ppa:ondrej/php && apt-get update -y

# apt-cache search php8.1 | grep "^php8.1" | cut -d' ' -f1 | sort
RUN apt-get install -y --no-install-recommends php8.1-amqp php8.1-bcmath php8.1-bz2 php8.1-cli php8.1-common \
    php8.1-curl php8.1-gd php8.1-gearman php8.1-gmp php8.1-gnupg php8.1-imagick php8.1-imap \
    php8.1-intl php8.1-mailparse php8.1-mbstring php8.1-memcache php8.1-memcached \
    php8.1-mongodb php8.1-msgpack php8.1-mysql php8.1-oauth php8.1-odbc php8.1-pcov php8.1-pgsql \
    php8.1-psr php8.1-readline php8.1-redis php8.1-snmp php8.1-soap php8.1-sqlite3 php8.1-ssh2 php8.1-uuid \
    php8.1-xdebug php8.1-xml php8.1-xmlrpc php8.1-xsl php8.1-yaml php8.1-zip php8.1-zmq
RUN apt-get dist-upgrade -y && apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/*

ADD conf.d/ /etc/php/8.1/cli/conf.d/
RUN mkdir /run/php/

# Composer v2
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer2
RUN composer2 self-update --2

# Composer v1
RUN cp -p /usr/bin/composer2 /usr/bin/composer1
RUN composer1 self-update --1

# Make Composer 2 the default
RUN ln -s /usr/bin/composer2 /usr/bin/composer
