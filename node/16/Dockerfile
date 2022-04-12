# docker build ./ -t magallanesci/node:16 --no-cache
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive \
    TZ=UTC

# Packages
RUN echo 'APT::Acquire::Retries "3";' > /etc/apt/apt.conf.d/80-retries
RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends ca-certificates curl gnupg git unzip
RUN curl -sL https://deb.nodesource.com/setup_16.x -o /tmp/nodesource_setup.sh  && \
    bash /tmp/nodesource_setup.sh && rm -f /tmp/nodesource_setup.sh && \
    apt install -y nodejs
RUN apt-get dist-upgrade -y && apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN npm install --global yarn

RUN mkdir /.npm && chmod 777 /.npm
