# docker-ownDynDNS-netcup

[![Worklfow](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup/badges/workflows/build_main.yaml/badge.svg)](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup) [![Release](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup/badges/release.svg)](https://git.smail.koeln/homelab/docker-ownDynDNS-netcup/releases) 

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
You need to create two dns entries beforehand:

| Host     | Type  | Destination  | 
|----------|-------|--------------|
| vpn      | AAAA  | IPv6         | 
| vpn      | A     | IPv4         |
| ddns     | AAAA  | IPv6         | 
| ddns     | A     | IPv4         |

vpn.example.com -> the domain that gets updated
ddns.example.com -> the domain your Fritz!Box calls for updates

## Container configuration
Create compose.yml and config in your app directory i.e.:

```
mkdir -p /opt/docker/owndyndns
cd /opt/docker/owndyndns

# Create docker-compose.yml and copy the contents from repository file
vi compose.yml

# Create config, copy the contents from repository example.config and change the parameters
vi config

# Start the Container with
docker compose up -d
```

## Fritz!Box configuration
* Login to your Fritz!Box
* Go to /Internet/Freigabe/DynDNS
* Set mark on "DynDNS benutzen"
* Enter Update-URL: `https://ddns.example.com/update.php?user=<username>&password=<pass>&ipv4=<ipaddr>&ipv6=<ip6addr>&domain=<domain>`
    * You only have to change `https://ddns.example.com` (http without valid TLS certificate)
* Domainname: `vpn.example.com`
* Username: Defined in config 
* Password: Defined in config
