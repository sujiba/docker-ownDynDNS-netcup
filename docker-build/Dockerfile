# Get latest app version
FROM alpine/git
WORKDIR /clone-workspace
RUN git clone https://github.com/fernwerker/ownDynDNS.git

# Build container to run the app
FROM php:apache

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y \
      libxml2-dev && \
    apt-get clean -y && \
    docker-php-ext-install soap  

WORKDIR /var/www/html
COPY --from=0 /clone-workspace/ownDynDNS /var/www/html
COPY --from=0 /clone-workspace/ownDynDNS/.htaccess.example /var/www/html/.htaccess

RUN chown -R www-data:www-data /var/www/html/
