# Get latest app version
FROM alpine:3.21.3
WORKDIR /clone-workspace
RUN apk update && \
    apk upgrade && \
    apk add git && \
    git clone https://github.com/fernwerker/ownDynDNS.git

# Build container to run the app
FROM php:8.4.6-apache
WORKDIR /var/www/html

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install --no-install-recommends -y \
      libxml2-dev && \
    docker-php-ext-install soap && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY --chown=www-data:www-data --from=0 /clone-workspace/ownDynDNS /var/www/html
COPY --chown=www-data:www-data --from=0 /clone-workspace/ownDynDNS/.htaccess.example /var/www/html/.htaccess
