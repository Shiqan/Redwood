# Redwood

### Docker Containers
* [Portainer](https://portainer.io "Portainer")

* [PIA](https://hub.docker.com/r/colinhebert/pia-openvpn/ "PIA")
  * [Transmission](https://hub.docker.com/r/linuxserver/transmission/ "Transmission")
  * [Jackett](https://github.com/Jackett/Jackett "Jackett")
  * [Radarr](https://github.com/Radarr/Radarr "Radarr")
  * [Sonarr](https://github.com/Sonarr/Sonarr "Sonarr")
  * [Lidarr](https://github.com/linuxserver/docker-lidarr "Lidarr") / [Headphones](https://github.com/rembo10/headphones "Headphones")
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
* [Change Cloud-init](#change-cloud-init)
* Mount hdd (`sudo fdisk -l` to see id, then `sudo mount /dev/id /mount/location`) and auto mount on boot (`sudo nano etc/fstab`), and grant access (`sudo chown -R user:group /mount/location/`)
* Change docker install to hdd (`sudo nano etc/default/docker`, add `-g /mount/location/docker`)
* Prepare `.env` file for docker-compose
* Build transmission proxy image (because of some weird issue with docker-compose build)
  * `cd proxy && docker build -t haugene/rpi-transmission-openvpn-proxy --file Dockerfile.armhf .`
* Run `docker-compose up -d`

#### Change Cloud-init 
* Change default username
* Change default password
* Change hostname
* Setup key-based authentication and disable password login
* See [Docs](http://cloudinit.readthedocs.io/en/latest/index.html) for more options (eg, you can also mount hdd)


#### Steps after installation
* Install a firewall (`sudo apt-get update && sudo apt-get install ufw`) and open the port(s) you want (eg,for ssh and plex: `sudo ufw allow ssh`, and `sudo ufw allow 32400/tcp`)
* Install fail2ban (`sudo apt-get install fail2ban`)
* Open port on router


#### Radarr & Sonarr Setup
* Add Indexers from Jackett (url `http://jacket:9117/...`)
* Add Transmission Download client (host: `transmission`)
* Redirect transmission `/data` folder to local `/downloads` folder


#### [DuckDNS Setup](https://www.duckdns.org/install.jsp)
* Create .sh script to make a request to the duckdns server (`echo url="https://www.duckdns.org/update?domains=exampledomain&token=a7c4d0ad-114e-40ef-ba1d-d217904a50f2&ip=" | curl -k -o ~/duckdns/duck.log -K -`)
* Add the .sh script to a cron job (`*/5 * * * * ~/duckdns/duck.sh >/dev/null 2>&1`)


#### [Discord notifications](https://blog.tiga.tech/discord-notifications-for-sonarr-radarr-and-lidarr/) 
* Add a discord webhook to a discord channel
* Add a slack webhook to Radarr/Sonarr
* Copy & past the discord webhook url and add `/slack` in the end (Discord will then interpret the webhook as Slack.)