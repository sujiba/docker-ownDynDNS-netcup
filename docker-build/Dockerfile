# Get latest app version
FROM alpine:3.20.1
WORKDIR /clone-workspace
RUN apk update && \
    apk upgrade && \
    apk add git && \
    git clone https://github.com/fernwerker/ownDynDNS.git

# Build container to run the app
FROM php:8.3.9-apache
WORKDIR /var/www/html

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
      libxml2-dev && \
    docker-php-ext-install soap && \
    apt-get clean -y

COPY --chown=www-data:www-data --from=0 /clone-workspace/ownDynDNS /var/www/html
COPY --chown=www-data:www-data --from=0 /clone-workspace/ownDynDNS/.htaccess.example /var/www/html/.htaccess
