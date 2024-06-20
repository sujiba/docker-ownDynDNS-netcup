# Get latest app version
FROM alpine:3.20.1
WORKDIR /clone-workspace
RUN apk update && \
    apk upgrade && \
    apk add git
RUN git clone https://github.com/fernwerker/ownDynDNS.git

# Build container to run the app
FROM php:8.3.8-apache
WORKDIR /var/www/html

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y \
      libxml2-dev
RUN docker-php-ext-install soap
RUN apt-get clean -y

COPY --from=0 /clone-workspace/ownDynDNS /var/www/html
COPY --from=0 /clone-workspace/ownDynDNS/.htaccess.example /var/www/html/.htaccess

RUN chown -R www-data:www-data /var/www/html/
