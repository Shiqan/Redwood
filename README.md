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
* Mount hdd (`sudo fdisk -l`) and auto mount on boot (`see etc/fstab`), and grant access (`sudo chown -R user:group /mount/location/`)
* Change docker install to hdd (`see etc/default/docker, -g /mount/location/docker`)
* Prepare `.env` file for docker-compose
* Build transmission proxy image (because of some weird issue with docker-compose build)
  * `cd proxy && docker build -t haugene/rpi-transmission-openvpn-proxy --file Dockerfile.armhf .`
* Run `docker-compose up -d`

#### Steps after installation (put it in the cloud-init)
* Change default username
* Change default password
* Change hostname
* Setup key-based authentication and disable password login
* Install a firewall (`sudo apt-get updaet && sudo apt-get install ufw`) and open the port(s) you want
* Install fail2ban (`sudo apt-get install fail2ban`)
* Open port on router

#### Radarr & Sonarr Setup
* Add Indexers from Jackett (url `http://jacket:9117/...`)
* Add Transmission Download client (host: `transmission`)
* Redirect transmission `/data` folder to local `/downloads` folder