# Redwood

### Docker Containers
* [Portainer](https://portainer.io "Portainer")

* [PIA](https://hub.docker.com/r/colinhebert/pia-openvpn/ "PIA")
  * [Transmission](https://hub.docker.com/r/linuxserver/transmission/ "Transmission")
  * [Jackett](https://github.com/Jackett/Jackett "Jackett")
  * [Radarr](https://github.com/Radarr/Radarr "Radarr")
  * [Sonarr](https://github.com/Sonarr/Sonarr "Sonarr")
  * [Headphones](https://github.com/rembo10/headphones "Headphones")
  * [Ombi](https://github.com/tidusjar/Ombi "Ombi")

* [Plex](https://plex.tv "Plex")
* [Tautulli](https://github.com/Tautulli/Tautulli "Tautulli")

<!-- * [Netdata](https://github.com/firehol/netdata "Netdata") -->
<!-- * [Pihole](https://pi-hole.net, "Pihole") -->
<!-- * [Pydio](https://pydio.com) -->




### Environment Variables
| Variable      | Use |
| ---           | --- |
| TZ            | Timezone |
| PGID          | Group ID |
| PUID          | User ID |
| PIA_USERNAME          | Private Internet Access username |
| PIA_PASSWORD          | Private Internet Access password  |
| PIA_REGION            | Private Internet Access region  |
| TRANSMISSION_WEB_UI   | Custom UI for Transmission  |

### Setup RPI

* Install [Hypriot](http://blog.hypriot.com/)
* Mount hdd (`sudo fdisk -l`) and auto mount on boot (`see etc/fstab`)
* Change docker install to hdd (`see etc/default/docker, -g /mnt/hdd/docker`)
* Prepare `.env` file for docker-compose
* Build transmission proxy image (because of some weird issue with docker-compose build)
  * `cd proxy && docker build -t haugene/rpi-transmission-openvpn-proxy --file Dockerfile.armhf .`
* Run `docker-compose up -d`