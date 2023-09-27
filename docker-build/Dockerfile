# Get latest app version
FROM alpine/git
WORKDIR /clone-workspace
RUN git clone https://github.com/fernwerker/ownDynDNS.git

# Build container to run the app
FROM php:apache
WORKDIR /var/www/html
COPY --from=0 /clone-workspace/ownDynDNS /var/www/html
