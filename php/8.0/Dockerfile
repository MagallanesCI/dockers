# docker build ./ -t magallanesci/php:8.0 --no-cache
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive \
    TZ=UTC

# Packages
RUN echo 'APT::Acquire::Retries "3";' > /etc/apt/apt.conf.d/80-retries
RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends locales ca-certificates curl git unzip software-properties-common gpg-agent
RUN add-apt-repository -y ppa:ondrej/php && apt-get update -y

# apt-cache search php8.0 | grep "^php8.0" | cut -d' ' -f1 | sort
RUN apt-get install -y --no-install-recommends php8.0-amqp php8.0-bcmath php8.0-bz2 php8.0-cli php8.0-common \
    php8.0-curl php8.0-gd php8.0-gearman php8.0-gmp php8.0-gnupg php8.0-imagick php8.0-imap \
    php8.0-intl php8.0-mailparse php8.0-mbstring php8.0-memcache php8.0-memcached \
    php8.0-mongodb php8.0-msgpack php8.0-mysql php8.0-oauth php8.0-odbc php8.0-pcov php8.0-pgsql \
    php8.0-psr php8.0-readline php8.0-redis php8.0-snmp php8.0-soap php8.0-sqlite3 php8.0-ssh2 php8.0-uuid \
    php8.0-xdebug php8.0-xml php8.0-xmlrpc php8.0-xsl php8.0-yaml php8.0-zip php8.0-zmq
RUN apt-get dist-upgrade -y && apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/*

ADD conf.d/ /etc/php/8.0/cli/conf.d/
RUN mkdir /run/php/

# Composer v1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer1
RUN composer1 self-update --1

# Composer v2
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer2
RUN composer2 self-update --2

# Make Composer 2 the default
RUN ln -s /usr/bin/composer2 /usr/bin/composer
