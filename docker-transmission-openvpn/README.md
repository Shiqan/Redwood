# Transmission & proxy image
See [haugene/docker-transmission-openvpn](https://github.com/haugene/docker-transmission-openvpn/blob/master/docker-compose-armhf.yml). Maybe one day he'll host the RPI images on docker hub as well, but for now, we'll have to build the images ourself.

* Build proxy image (because of some weird issue with docker-compose)
  * `cd proxy && docker build -t haugene/rpi-transmission-openvpn-proxy --file Dockerfile.armhf .`