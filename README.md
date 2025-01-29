# docker-ownDynDNS-netcup

[![Worklfow](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup/badges/workflows/build_main.yaml/badge.svg)](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup) [![Release](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup/badges/release.svg)](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup) 

- [docker-ownDynDNS-netcup](#docker-owndyndns-netcup)
  - [acknowledgments](#acknowledgments)
  - [Netcup configuration](#netcup-configuration)
  - [Container configuration](#container-configuration)
  - [Fritz!Box configuration](#fritzbox-configuration)

## acknowledgments

This container is based on the work of:
* [Docker PHP](https://hub.docker.com/_/php)
* [Fernwerker ownDynDNS](https://github.com/fernwerker/ownDynDNS)

## Netcup configuration
You need to create your dns entries beforehand:

| Host     | Type  | Destination  |
|----------|-------|--------------|
| vpn      | AAAA  | IPv6         |
| vpn      | A     | IPv4         |

## Container configuration
Create docker-compose.yml and config in your app directory i.e.:

```
mkdir -p /opt/docker/owndyndns
cd /opt/docker/owndyndns

# Create docker-compose.yml and copy the contents from repository file
vi docker-compose.yml

# Create config, copy the contents from repository example.config and change the parameters
vi config

# Start the Container with
docker compose up -d
```

## Fritz!Box configuration
* Login to your Fritz!Box
* Go to /Internet/Freigabe/DynDNS
* Set mark on "DynDNS benutzen"
* Enter Update-URL: `https://<url of your webspace>/update.php?user=<username>&password=<pass>&ipv4=<ipaddr>&ipv6=<ip6addr>&domain=<domain>`
    * You only have to change `https://<url of your webspace>` (http without valid TLS certificate)
* Domainname: `vpn.example.com`
* Username: Defined in config 
* Password: Defined in config
