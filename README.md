# 🎛️ Awesome Homelab FOSS Containers

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Self-Hosted](https://img.shields.io/badge/Self--Hosted-Homelab-blueviolet?logo=linux&logoColor=white)](https://github.com/)
[![Tailscale](https://img.shields.io/badge/Tailscale-Protected-2A2B36?logo=tailscale&logoColor=white)](https://tailscale.com/)

A list of **Free and Open Source Software (FOSS)** container stacks that I handpicked and tested for homelab.

---

## 📑 Table of Contents

- [🛠️ Management & Monitoring](#️-management--monitoring)
  - [Portainer](#portainer)
  - [Cloud Commander](#cloud-commander)
  - [Glances](#glances)
  - [Uptime Kuma](#uptime-kuma)
- [📊 Dashboard](#-dashboard)
  - [Homepage](#homepage)
- [🏠 Home Automation](#-home-automation)
  - [Home Assistant](#home-assistant)
- [🎬 Media Streaming & Libraries](#-media-streaming--libraries)
  - [Jellyfin](#jellyfin)
  - [Audiobookshelf](#audiobookshelf)
  - [Navidrome](#navidrome)
  - [Explo](#explo)
  - [Aurral](#aurral)
- [⬇️ Automation & Downloaders](#️-automation--downloaders)
  - [Sonarr](#sonarr)
  - [Radarr](#radarr)
  - [Lidarr](#lidarr)
  - [Prowlarr](#prowlarr)
  - [Jackett](#jackett)
  - [Jellyseerr](#jellyseerr)
  - [qBittorrent](#qbittorrent)
  - [SABnzbd](#sabnzbd)
  - [FlareSolverr](#flaresolverr)
- [📚 Books, Audiobooks & Manga](#-books-audiobooks--manga)
  - [Readarr](#readarr)
  - [Kavita](#kavita)
- [📸 Photos, Cloud & Sync](#-photos-cloud--sync)
  - [Immich Stack](#immich-stack)
  - [gPhotos2Immich](#gphotos2immich)
  - [Nextcloud Stack](#nextcloud-stack)
- [🔒 Authentication, Reverse Proxy & Ingress](#-authentication-reverse-proxy--ingress)
  - [Authelia SSO](#authelia-sso)
  - [Caddy Reverse Proxy](#caddy-reverse-proxy)
- [💾 Backup & Disaster Recovery](#-backup--disaster-recovery)
  - [Backrest (Restic Web UI)](#backrest-restic-web-ui)

---

## 🛠️ Management & Monitoring

### Portainer
Docker management UI - start/stop containers, stacks and volumes without the CLI.

[![Portainer](https://github-readme-stats-fast.vercel.app/api/pin/?username=portainer&repo=portainer&theme=dark)](https://github.com/portainer/portainer)<br>
![last commit](https://badgen.net/github/last-commit/portainer/portainer) ![release](https://badgen.net/github/release/portainer/portainer) ![released](https://img.shields.io/github/release-date/portainer/portainer?style=flat&label=released)

**Links:** [Official Site](https://www.portainer.io/) | [Docker Hub](https://hub.docker.com/r/portainer/portainer-ce) | [Docs](https://docs.portainer.io/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ${CONFIG_ROOT}/portainer:/data
    ports:
      - "9000:9000"
    networks:
      - homelab_net
```
</details>

---

### Cloud Commander
Somewhat simplistic dual-panel web file manager with in-browser editor and console support.

Picked over filestash cause it's text editor is easier to use for casual windows user.

[![Cloud Commander](https://github-readme-stats-fast.vercel.app/api/pin/?username=coderaiser&repo=cloudcmd&theme=dark)](https://github.com/coderaiser/cloudcmd)<br>
![last commit](https://badgen.net/github/last-commit/coderaiser/cloudcmd) ![release](https://badgen.net/github/release/coderaiser/cloudcmd) ![released](https://img.shields.io/github/release-date/coderaiser/cloudcmd?style=flat&label=released)

**Links:** [Official Site](https://cloudcmd.io/) | [Docker Hub](https://hub.docker.com/r/coderaiser/cloudcmd) | [Docs](https://cloudcmd.io/#documentation)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  cloudcmd:
    image: coderaiser/cloudcmd:latest
    container_name: cloudcmd
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
    volumes:
      - ${DATA_ROOT}:/mnt/fs
      - ${CONFIG_ROOT}/cloudcmd:/root
    ports:
      - "8000:8000"
    networks:
      - homelab_net
```
</details>

---

### Glances
Terminal UI task monitoring to help you see what processes are eating resources.

[![Glances](https://github-readme-stats-fast.vercel.app/api/pin/?username=nicolargo&repo=glances&theme=dark)](https://github.com/nicolargo/glances)<br>
![last commit](https://badgen.net/github/last-commit/nicolargo/glances) ![release](https://badgen.net/github/release/nicolargo/glances) ![released](https://img.shields.io/github/release-date/nicolargo/glances?style=flat&label=released)

**Links:** [Official Site](https://nicolargo.github.io/glances/) | [Docker Hub](https://hub.docker.com/r/nicolargo/glances) | [Docs](https://glances.readthedocs.io/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  glances:
    image: nicolargo/glances:latest
    container_name: glances
    restart: unless-stopped
    pid: host
    environment:
      - GLANCES_OPT=-w
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ${CONFIG_ROOT}/glances:/glances/conf
    ports:
      - "61208:61208"
    networks:
      - homelab_net
```
</details>

---

### Uptime Kuma
Uptime monitoring for containers.

[![Uptime Kuma](https://github-readme-stats-fast.vercel.app/api/pin/?username=louislam&repo=uptime-kuma&theme=dark)](https://github.com/louislam/uptime-kuma)<br>
![last commit](https://badgen.net/github/last-commit/louislam/uptime-kuma) ![release](https://badgen.net/github/release/louislam/uptime-kuma) ![released](https://img.shields.io/github/release-date/louislam/uptime-kuma?style=flat&label=released)

**Links:** [Official Site](https://uptime.kuma.pet/) | [Docker Hub](https://hub.docker.com/r/louislam/uptime-kuma) | [Docs](https://github.com/louislam/uptime-kuma/wiki)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    restart: unless-stopped
    volumes:
      - ${CONFIG_ROOT}/uptime-kuma:/app/data
      - /var/run/docker.sock:/var/run/docker.sock:ro
    ports:
      - "3002:3001"
    networks:
      - homelab_net
```
</details>

---

## 📊 Dashboard

### Homepage
Start page - one dashboard with links and live widgets for all services.

[![Homepage](https://github-readme-stats-fast.vercel.app/api/pin/?username=gethomepage&repo=homepage&theme=dark)](https://github.com/gethomepage/homepage)<br>
![last commit](https://badgen.net/github/last-commit/gethomepage/homepage) ![release](https://badgen.net/github/release/gethomepage/homepage) ![released](https://img.shields.io/github/release-date/gethomepage/homepage?style=flat&label=released)

**Links:** [Official Site](https://gethomepage.dev/) | [GitHub Container Registry](https://ghcr.io/gethomepage/homepage) | [Docs](https://gethomepage.dev/installation/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/homepage/config:/app/config
      - /var/run/docker.sock:/var/run/docker.sock:ro
    ports:
      - "3000:3000"
    networks:
      - homelab_net
```
</details>

---

## 🏠 Home Automation

### Home Assistant
Open-source home automation hub.
Zigbee dongle is reasonable upgrade, if your homelab not support Zigbee.

[![Home Assistant Core](https://github-readme-stats-fast.vercel.app/api/pin/?username=home-assistant&repo=core&theme=dark)](https://github.com/home-assistant/core)<br>
![last commit](https://badgen.net/github/last-commit/home-assistant/core) ![release](https://badgen.net/github/release/home-assistant/core) ![released](https://img.shields.io/github/release-date/home-assistant/core?style=flat&label=released)

**Links:** [Official Site](https://www.home-assistant.io/) | [GHCR](https://ghcr.io/home-assistant/home-assistant) | [Docs](https://www.home-assistant.io/docs/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  homeassistant:
    image: ghcr.io/home-assistant/home-assistant:stable
    container_name: homeassistant
    restart: unless-stopped
    privileged: true
    environment:
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/homeassistant:/config
      - /etc/localtime:/etc/localtime:ro
      - /run/dbus:/run/dbus:ro
    ports:
      - "8123:8123"
    networks:
      - homelab_net
```
</details>

---

## 🎬 Media Streaming & Libraries

### Jellyfin
Plex/Netflix alternative - streams movies, TV and music to any device.

[![Jellyfin](https://github-readme-stats-fast.vercel.app/api/pin/?username=jellyfin&repo=jellyfin&theme=dark)](https://github.com/jellyfin/jellyfin)<br>
![last commit](https://badgen.net/github/last-commit/jellyfin/jellyfin) ![release](https://badgen.net/github/release/jellyfin/jellyfin) ![released](https://img.shields.io/github/release-date/jellyfin/jellyfin?style=flat&label=released)

**Links:** [Official Site](https://jellyfin.org/) | [Docker Hub](https://hub.docker.com/r/jellyfin/jellyfin) | [Docs](https://jellyfin.org/docs/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    restart: unless-stopped
    user: ${PUID}:${PGID}
    environment:
      - TZ=${TZ}
      - JELLYFIN_PublishedServerUrl=http://${SERVER_IP}:8096
    volumes:
      - ${CONFIG_ROOT}/jellyfin:/config
      - ${CONFIG_ROOT}/jellyfin-cache:/cache
      - ${MEDIA_ROOT}/movies:/movies:ro
      - ${MEDIA_ROOT}/tv:/tv:ro
      - ${MEDIA_ROOT}/anime:/anime:ro
      - ${MEDIA_ROOT}/music:/music:ro
    ports:
      - "8096:8096"
    networks:
      - homelab_net
```
</details>

---

### Audiobookshelf
Audible alternative - audiobooks and podcasts with per-user progress sync.

[![Audiobookshelf](https://github-readme-stats-fast.vercel.app/api/pin/?username=advplyr&repo=audiobookshelf&theme=dark)](https://github.com/advplyr/audiobookshelf)<br>
![last commit](https://badgen.net/github/last-commit/advplyr/audiobookshelf) ![release](https://badgen.net/github/release/advplyr/audiobookshelf) ![released](https://img.shields.io/github/release-date/advplyr/audiobookshelf?style=flat&label=released)

**Links:** [Official Site](https://www.audiobookshelf.org/) | [GHCR](https://ghcr.io/advplyr/audiobookshelf) | [Docs](https://www.audiobookshelf.org/docs)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  audiobookshelf:
    image: ghcr.io/advplyr/audiobookshelf:latest
    container_name: audiobookshelf
    restart: unless-stopped
    environment:
      - AUDIOBOOKSHELF_UID=${PUID}
      - AUDIOBOOKSHELF_GID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/audiobookshelf/config:/config
      - ${CONFIG_ROOT}/audiobookshelf/metadata:/metadata
      - ${MEDIA_ROOT}/audiobooks:/audiobooks
      - ${MEDIA_ROOT}/podcasts:/podcasts
    ports:
      - "13378:80"
    networks:
      - homelab_net
```
</details>

---

### Navidrome
Spotify alternative - streams a self-hosted music library to phone and desktop apps.

[![Navidrome](https://github-readme-stats-fast.vercel.app/api/pin/?username=deluan&repo=navidrome&theme=dark)](https://github.com/deluan/navidrome)<br>
![last commit](https://badgen.net/github/last-commit/deluan/navidrome) ![release](https://badgen.net/github/release/deluan/navidrome) ![released](https://img.shields.io/github/release-date/deluan/navidrome?style=flat&label=released)

**Links:** [Official Site](https://www.navidrome.org/) | [Docker Hub](https://hub.docker.com/r/deluan/navidrome) | [Docs](https://www.navidrome.org/docs/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  navidrome:
    image: deluan/navidrome:latest
    container_name: navidrome
    restart: unless-stopped
    user: ${PUID}:${PGID}
    environment:
      - ND_SCANSCHEDULE=1h
      - ND_LOGLEVEL=info
      - ND_BASEURL=/navidrome
      - ND_ENABLETRANSCODINGCONFIG=true
    volumes:
      - ${CONFIG_ROOT}/navidrome:/data
      - ${MEDIA_ROOT}/music:/music:ro
    ports:
      - "4533:4533"
    networks:
      - homelab_net
```
</details>

---

### Explo
Discover Weekly alternative - suggests new music from listening history.

[![Explo](https://github-readme-stats-fast.vercel.app/api/pin/?username=LumePart&repo=Explo&theme=dark)](https://github.com/LumePart/Explo)<br>
![last commit](https://badgen.net/github/last-commit/LumePart/Explo) ![release](https://badgen.net/github/release/LumePart/Explo) ![released](https://img.shields.io/github/release-date/LumePart/Explo?style=flat&label=released)

**Links:** [GitHub Container Registry](https://ghcr.io/lumepart/explo)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  explo:
    image: ghcr.io/lumepart/explo:latest
    container_name: explo
    restart: unless-stopped
    environment:
      - PORT=7288
      - NODE_ENV=production
    volumes:
      - ${CONFIG_ROOT}/explo:/app/data
    ports:
      - "7288:7288"
    networks:
      - homelab_net
```
</details>

---

### Aurral
Music discovery that feeds recommended tracks into the music library.

[![Aurral](https://github-readme-stats-fast.vercel.app/api/pin/?username=lklynet&repo=aurral&theme=dark)](https://github.com/lklynet/aurral)<br>
![last commit](https://badgen.net/github/last-commit/lklynet/aurral) ![release](https://badgen.net/github/release/lklynet/aurral) ![released](https://img.shields.io/github/release-date/lklynet/aurral?style=flat&label=released)

**Links:** [GitHub Container Registry](https://ghcr.io/lklynet/aurral)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  aurral:
    image: ghcr.io/lklynet/aurral:latest
    container_name: aurral
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/aurral:/config
    ports:
      - "3001:3001"
    networks:
      - homelab_net
```
</details>

---

## ⬇️ Automation & Downloaders

### Sonarr
Monitors for new episodes of TV shows and anime, then downloads them automatically.

[![Sonarr](https://github-readme-stats-fast.vercel.app/api/pin/?username=Sonarr&repo=Sonarr&theme=dark)](https://github.com/Sonarr/Sonarr)<br>
![last commit](https://badgen.net/github/last-commit/Sonarr/Sonarr) ![release](https://badgen.net/github/release/Sonarr/Sonarr) ![released](https://img.shields.io/github/release-date/Sonarr/Sonarr?style=flat&label=released)

**Links:** [Official Site](https://sonarr.tv/) | [Docker Hub](https://hub.docker.com/r/linuxserver/sonarr) | [Docs](https://wiki.servarr.com/sonarr)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/sonarr:/config
      - ${MEDIA_ROOT}/tv:/tv
      - ${MEDIA_ROOT}/anime:/anime
      - ${DATA_ROOT}/downloads:/downloads
    ports:
      - "127.0.0.1:8989:8989"
    networks:
      - homelab_net
```
</details>

---

### Radarr
Monitors for movies and downloads them automatically.

[![Radarr](https://github-readme-stats-fast.vercel.app/api/pin/?username=Radarr&repo=Radarr&theme=dark)](https://github.com/Radarr/Radarr)<br>
![last commit](https://badgen.net/github/last-commit/Radarr/Radarr) ![release](https://badgen.net/github/release/Radarr/Radarr) ![released](https://img.shields.io/github/release-date/Radarr/Radarr?style=flat&label=released)

**Links:** [Official Site](https://radarr.video/) | [Docker Hub](https://hub.docker.com/r/linuxserver/radarr) | [Docs](https://wiki.servarr.com/radarr)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/radarr:/config
      - ${MEDIA_ROOT}/movies:/movies
      - ${DATA_ROOT}/downloads:/downloads
    ports:
      - "127.0.0.1:7878:7878"
    networks:
      - homelab_net
```
</details>

---

### Lidarr
Monitors for albums and downloads them automatically.

[![Lidarr](https://github-readme-stats-fast.vercel.app/api/pin/?username=Lidarr&repo=Lidarr&theme=dark)](https://github.com/Lidarr/Lidarr)<br>
![last commit](https://badgen.net/github/last-commit/Lidarr/Lidarr) ![release](https://badgen.net/github/release/Lidarr/Lidarr) ![released](https://img.shields.io/github/release-date/Lidarr/Lidarr?style=flat&label=released)

**Links:** [Official Site](https://lidarr.audio/) | [Docker Hub](https://hub.docker.com/r/linuxserver/lidarr) | [Docs](https://wiki.servarr.com/lidarr)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  lidarr:
    image: lscr.io/linuxserver/lidarr:latest
    container_name: lidarr
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/lidarr:/config
      - ${MEDIA_ROOT}/music:/music
      - ${DATA_ROOT}/downloads:/downloads
    ports:
      - "127.0.0.1:8686:8686"
    networks:
      - homelab_net
```
</details>

---

### Prowlarr
Collects indexers and shares their search results with the download automators.

[![Prowlarr](https://github-readme-stats-fast.vercel.app/api/pin/?username=Prowlarr&repo=Prowlarr&theme=dark)](https://github.com/Prowlarr/Prowlarr)<br>
![last commit](https://badgen.net/github/last-commit/Prowlarr/Prowlarr) ![release](https://badgen.net/github/release/Prowlarr/Prowlarr) ![released](https://img.shields.io/github/release-date/Prowlarr/Prowlarr?style=flat&label=released)

**Links:** [Official Site](https://prowlarr.com/) | [Docker Hub](https://hub.docker.com/r/linuxserver/prowlarr) | [Docs](https://wiki.servarr.com/prowlarr)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/prowlarr:/config
    ports:
      - "127.0.0.1:9696:9696"
    networks:
      - homelab_net
```
</details>

---

### Jackett
Torrent-indexer proxy that supplies search results to the download automators.

[![Jackett](https://github-readme-stats-fast.vercel.app/api/pin/?username=Jackett&repo=Jackett&theme=dark)](https://github.com/Jackett/Jackett)<br>
![last commit](https://badgen.net/github/last-commit/Jackett/Jackett) ![release](https://badgen.net/github/release/Jackett/Jackett) ![released](https://img.shields.io/github/release-date/Jackett/Jackett?style=flat&label=released)

**Links:** [Docker Hub](https://hub.docker.com/r/linuxserver/jackett) | [Docs](https://github.com/Jackett/Jackett#readme)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  jackett:
    image: lscr.io/linuxserver/jackett:latest
    container_name: jackett
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/jackett:/config
      - ${DATA_ROOT}/downloads:/downloads
    ports:
      - "127.0.0.1:9117:9117"
    networks:
      - homelab_net
```
</details>

---

### Jellyseerr
Request page so others can ask for movies and shows to be added.

[![Jellyseerr](https://github-readme-stats-fast.vercel.app/api/pin/?username=fallenbagel&repo=jellyseerr&theme=dark)](https://github.com/fallenbagel/jellyseerr)<br>
![last commit](https://badgen.net/github/last-commit/fallenbagel/jellyseerr) ![release](https://badgen.net/github/release/fallenbagel/jellyseerr) ![released](https://img.shields.io/github/release-date/fallenbagel/jellyseerr?style=flat&label=released)

**Links:** [Official Site](https://github.com/fallenbagel/jellyseerr) | [Docker Hub](https://hub.docker.com/r/fallenbagel/jellyseerr) | [Docs](https://docs.jellyseerr.dev/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  jellyseerr:
    image: fallenbagel/jellyseerr:latest
    container_name: jellyseerr
    restart: unless-stopped
    environment:
      - LOG_LEVEL=debug
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/jellyseerr:/app/config
    ports:
      - "5055:5055"
    networks:
      - homelab_net
```
</details>

---

### qBittorrent
Torrent download client the download automators send their grabs to.

[![qBittorrent](https://github-readme-stats-fast.vercel.app/api/pin/?username=qbittorrent&repo=qBittorrent&theme=dark)](https://github.com/qbittorrent/qBittorrent)<br>
![last commit](https://badgen.net/github/last-commit/qbittorrent/qBittorrent) ![release](https://badgen.net/github/release/qbittorrent/qBittorrent) ![released](https://img.shields.io/github/release-date/qbittorrent/qBittorrent?style=flat&label=released)

**Links:** [Official Site](https://www.qbittorrent.org/) | [Docker Hub](https://hub.docker.com/r/linuxserver/qbittorrent) | [Docs](https://github.com/qbittorrent/qBittorrent/wiki)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
      - WEBUI_PORT=8080
    volumes:
      - ${CONFIG_ROOT}/qbittorrent:/config
      - ${DATA_ROOT}/downloads:/downloads
    ports:
      - "127.0.0.1:8080:8080"
      - "6881:6881"
      - "6881:6881/udp"
    networks:
      - homelab_net
```
</details>

---

### SABnzbd
Usenet download client for the download automators.

[![SABnzbd](https://github-readme-stats-fast.vercel.app/api/pin/?username=sabnzbd&repo=sabnzbd&theme=dark)](https://github.com/sabnzbd/sabnzbd)<br>
![last commit](https://badgen.net/github/last-commit/sabnzbd/sabnzbd) ![release](https://badgen.net/github/release/sabnzbd/sabnzbd) ![released](https://img.shields.io/github/release-date/sabnzbd/sabnzbd?style=flat&label=released)

**Links:** [Official Site](https://sabnzbd.org/) | [Docker Hub](https://hub.docker.com/r/linuxserver/sabnzbd) | [Docs](https://sabnzbd.org/wiki/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  sabnzbd:
    image: lscr.io/linuxserver/sabnzbd:latest
    container_name: sabnzbd
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/sabnzbd:/config
      - ${DATA_ROOT}/downloads:/downloads
    ports:
      - "127.0.0.1:8085:8080"
    networks:
      - homelab_net
```
</details>

---

### FlareSolverr
Gets indexers past Cloudflare so the indexer tools keep working.

[![FlareSolverr](https://github-readme-stats-fast.vercel.app/api/pin/?username=FlareSolverr&repo=FlareSolverr&theme=dark)](https://github.com/FlareSolverr/FlareSolverr)<br>
![last commit](https://badgen.net/github/last-commit/FlareSolverr/FlareSolverr) ![release](https://badgen.net/github/release/FlareSolverr/FlareSolverr) ![released](https://img.shields.io/github/release-date/FlareSolverr/FlareSolverr?style=flat&label=released)

**Links:** [Docker Hub](https://hub.docker.com/r/flaresolverr/flaresolverr) | [Docs](https://github.com/FlareSolverr/FlareSolverr#readme)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  flaresolverr:
    image: flaresolverr/flaresolverr:latest
    container_name: flaresolverr
    restart: unless-stopped
    environment:
      - LOG_LEVEL=info
      - LOG_HTML=false
      - CAPTCHA_SOLVER=none
      - TZ=${TZ}
    ports:
      - "127.0.0.1:8191:8191"
    networks:
      - homelab_net
```
</details>

---

## 📚 Books, Audiobooks & Manga

### Readarr
Monitors for books and audiobooks and downloads them automatically.

[![Readarr](https://github-readme-stats-fast.vercel.app/api/pin/?username=Readarr&repo=Readarr&theme=dark)](https://github.com/Readarr/Readarr)<br>
![last commit](https://badgen.net/github/last-commit/Readarr/Readarr) ![release](https://badgen.net/github/release/Readarr/Readarr) ![released](https://img.shields.io/github/release-date/Readarr/Readarr?style=flat&label=released)

**Links:** [Official Site](https://readarr.com/) | [Docker Hub](https://hub.docker.com/r/linuxserver/readarr) | [Docs](https://wiki.servarr.com/readarr)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  readarr:
    image: lscr.io/linuxserver/readarr:develop
    container_name: readarr
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/readarr:/config
      - ${DATA_ROOT}/books:/books
      - ${MEDIA_ROOT}/audiobooks:/audiobooks
      - ${DATA_ROOT}/downloads:/downloads
    ports:
      - "127.0.0.1:8787:8787"
    networks:
      - homelab_net
```
</details>

---

### Kavita
Kindle alternative - reads manga, comics and e-books in the browser.

[![Kavita](https://github-readme-stats-fast.vercel.app/api/pin/?username=Kareadita&repo=Kavita&theme=dark)](https://github.com/Kareadita/Kavita)<br>
![last commit](https://badgen.net/github/last-commit/Kareadita/Kavita) ![release](https://badgen.net/github/release/Kareadita/Kavita) ![released](https://img.shields.io/github/release-date/Kareadita/Kavita?style=flat&label=released)

**Links:** [Official Site](https://www.kavitareader.com/) | [Docker Hub](https://hub.docker.com/r/jvmilazz0/kavita) | [Docs](https://wiki.kavitareader.com/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  kavita:
    image: jvmilazz0/kavita:latest
    container_name: kavita
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/kavita:/kavita/config
      - ${DATA_ROOT}/books:/kavita/data/books
    ports:
      - "5000:5000"
    networks:
      - homelab_net
```
</details>

---

## 📸 Photos, Cloud & Sync

### Immich Stack
Google Photos alternative - backs up photos/videos with face and object search.

[![Immich](https://github-readme-stats-fast.vercel.app/api/pin/?username=immich-app&repo=immich&theme=dark)](https://github.com/immich-app/immich)<br>
![last commit](https://badgen.net/github/last-commit/immich-app/immich) ![release](https://badgen.net/github/release/immich-app/immich) ![released](https://img.shields.io/github/release-date/immich-app/immich?style=flat&label=released)

**Links:** [Official Site](https://immich.app/) | [GitHub Container Registry](https://ghcr.io/immich-app/immich-server) | [Docs](https://immich.app/docs)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  immich-server:
    image: ghcr.io/immich-app/immich-server:release
    container_name: immich_server
    restart: unless-stopped
    volumes:
      - ${MEDIA_ROOT}/photos:/usr/src/app/upload
      - /etc/localtime:/etc/localtime:ro
    environment:
      - DB_HOSTNAME=immich_postgres
      - DB_USERNAME=postgres
      - DB_PASSWORD=${IMMICH_DB_PASSWORD}
      - DB_DATABASE_NAME=immich
      - REDIS_HOSTNAME=immich_redis
    ports:
      - "2283:2283"
    depends_on:
      - immich-redis
      - immich-postgres
    networks:
      - immich_net
      - homelab_net

  immich-machine-learning:
    image: ghcr.io/immich-app/immich-machine-learning:release
    container_name: immich_machine_learning
    restart: unless-stopped
    volumes:
      - ${CONFIG_ROOT}/immich/cache:/cache
    environment:
      - DB_HOSTNAME=immich_postgres
      - DB_USERNAME=postgres
      - DB_PASSWORD=${IMMICH_DB_PASSWORD}
      - DB_DATABASE_NAME=immich
      - REDIS_HOSTNAME=immich_redis
    networks:
      - immich_net

  immich-redis:
    image: redis:6.2-alpine
    container_name: immich_redis
    restart: unless-stopped
    networks:
      - immich_net

  immich-postgres:
    image: tensorchord/pgvecto-rs:pg14-v0.2.0
    container_name: immich_postgres
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=${IMMICH_DB_PASSWORD}
      - POSTGRES_USER=postgres
      - POSTGRES_DB=immich
      - POSTGRES_INITDB_ARGS=--data-checksums
    volumes:
      - ${CONFIG_ROOT}/immich/postgres:/var/lib/postgresql/data
    networks:
      - immich_net

networks:
  immich_net:
    name: immich_net
  homelab_net:
    name: homelab_net
    external: true
```
</details>

---

### gPhotos2Immich
Pulls Google Photos albums into the self-hosted photo library automatically.

[![gPhotos2Immich](https://github-readme-stats-fast.vercel.app/api/pin/?username=warreth&repo=gPhotos2Immich&theme=dark)](https://github.com/warreth/gPhotos2Immich)<br>
![last commit](https://badgen.net/github/last-commit/warreth/gPhotos2Immich) ![release](https://badgen.net/github/release/warreth/gPhotos2Immich) ![released](https://img.shields.io/github/release-date/warreth/gPhotos2Immich?style=flat&label=released)

**Links:** [GitHub Container Registry](https://ghcr.io/warreth/gphotos2immich) | [Docs](https://github.com/warreth/gPhotos2Immich#readme)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  gphotos2immich:
    image: ghcr.io/warreth/gphotos2immich:latest
    container_name: gphotos2immich
    restart: unless-stopped
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
      - CRON_SCHEDULE=0 3 * * *
    volumes:
      - ${CONFIG_ROOT}/gphotos2immich/config.json:/app/config.json:ro
    networks:
      - homelab_net
```
</details>

---

### Nextcloud Stack
Google Drive/Dropbox alternative - files, calendar, contacts and docs.

[![Nextcloud](https://github-readme-stats-fast.vercel.app/api/pin/?username=nextcloud&repo=server&theme=dark)](https://github.com/nextcloud/server)<br>
![last commit](https://badgen.net/github/last-commit/nextcloud/server) ![release](https://badgen.net/github/release/nextcloud/server) ![released](https://img.shields.io/github/release-date/nextcloud/server?style=flat&label=released)

**Links:** [Official Site](https://nextcloud.com/) | [Docker Hub](https://hub.docker.com/_/nextcloud) | [Docs](https://docs.nextcloud.com/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  nextcloud:
    image: nextcloud:apache
    container_name: nextcloud
    restart: unless-stopped
    depends_on:
      - nextcloud-db
      - nextcloud-redis
    environment:
      - POSTGRES_HOST=nextcloud-db
      - POSTGRES_DB=nextcloud
      - POSTGRES_USER=nextcloud
      - POSTGRES_PASSWORD=${NEXTCLOUD_DB_PASSWORD}
      - REDIS_HOST=nextcloud-redis
      - OVERWRITEWEBROOT=/nextcloud
      - OVERWRITEPROTOCOL=https
    volumes:
      - ${CONFIG_ROOT}/nextcloud/html:/var/www/html
      - ${DATA_ROOT}/nextcloud-data:/var/www/html/data
    ports:
      - "8080:80"
    networks:
      - homelab_net

  nextcloud-db:
    image: postgres:15-alpine
    container_name: nextcloud-db
    restart: unless-stopped
    environment:
      - POSTGRES_DB=nextcloud
      - POSTGRES_USER=nextcloud
      - POSTGRES_PASSWORD=${NEXTCLOUD_DB_PASSWORD}
    volumes:
      - ${CONFIG_ROOT}/nextcloud/db:/var/lib/postgresql/data
    networks:
      - homelab_net

  nextcloud-redis:
    image: redis:alpine
    container_name: nextcloud-redis
    restart: unless-stopped
    networks:
      - homelab_net
```
</details>

---

## 🔒 Authentication, Reverse Proxy & Ingress

### Authelia SSO
Single sign-on for containers, to login less in each container individually. Still not supported in many places, so not resolve login completely.

[![Authelia](https://github-readme-stats-fast.vercel.app/api/pin/?username=authelia&repo=authelia&theme=dark)](https://github.com/authelia/authelia)<br>
![last commit](https://badgen.net/github/last-commit/authelia/authelia) ![release](https://badgen.net/github/release/authelia/authelia) ![released](https://img.shields.io/github/release-date/authelia/authelia?style=flat&label=released)

**Links:** [Official Site](https://www.authelia.com/) | [Docker Hub](https://hub.docker.com/r/authelia/authelia) | [Docs](https://www.authelia.com/docs/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  authelia:
    image: authelia/authelia:latest
    container_name: authelia
    restart: unless-stopped
    environment:
      - TZ=${TZ}
      - AUTHELIA_JWT_SECRET=${AUTHELIA_JWT_SECRET}
      - AUTHELIA_STORAGE_ENCRYPTION_KEY=${AUTHELIA_STORAGE_ENCRYPTION_KEY}
      - AUTHELIA_SESSION_SECRET=${AUTHELIA_SESSION_SECRET}
    volumes:
      - ${CONFIG_ROOT}/authelia:/config
    ports:
      - "9091:9091"
    networks:
      - homelab_net
```
</details>

---

### Caddy Reverse Proxy
Reverse proxy that gives services domains and automatic HTTPS.

[![Caddy](https://github-readme-stats-fast.vercel.app/api/pin/?username=caddyserver&repo=caddy&theme=dark)](https://github.com/caddyserver/caddy)<br>
![last commit](https://badgen.net/github/last-commit/caddyserver/caddy) ![release](https://badgen.net/github/release/caddyserver/caddy) ![released](https://img.shields.io/github/release-date/caddyserver/caddy?style=flat&label=released)

**Links:** [Official Site](https://caddyserver.com/) | [Docker Hub](https://hub.docker.com/_/caddy) | [Docs](https://caddyserver.com/docs/)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  caddy-auth:
    image: caddy:alpine
    container_name: caddy-auth
    restart: unless-stopped
    environment:
      - DOMAIN_NAME=${DOMAIN_NAME}
    volumes:
      - ${CONFIG_ROOT}/caddy/Caddyfile:/etc/caddy/Caddyfile:ro
      - ${CONFIG_ROOT}/caddy/data:/data
      - ${CONFIG_ROOT}/caddy/config:/config
    ports:
      - "80:80"
      - "443:443"
    networks:
      - homelab_net
```
</details>

---

## 💾 Backup & Disaster Recovery

### Backrest (Restic Web UI)
Web UI for Restic backups - schedules, retention and restores.

[![Backrest](https://github-readme-stats-fast.vercel.app/api/pin/?username=garethgeorge&repo=backrest&theme=dark)](https://github.com/garethgeorge/backrest)<br>
![last commit](https://badgen.net/github/last-commit/garethgeorge/backrest) ![release](https://badgen.net/github/release/garethgeorge/backrest) ![released](https://img.shields.io/github/release-date/garethgeorge/backrest?style=flat&label=released)

**Links:** [Official Site](https://github.com/garethgeorge/backrest) | [Docker Hub](https://hub.docker.com/r/garethgeorge/backrest) | [Docs](https://github.com/garethgeorge/backrest#documentation)

<details>
<summary>Docker Compose Example</summary>

```yaml
services:
  backrest:
    image: garethgeorge/backrest:v1.14.1
    container_name: backrest
    restart: unless-stopped
    environment:
      - BACKREST_CONFIG=/config/config.json
      - BACKREST_DATA=/data
      - TZ=${TZ}
    volumes:
      - ${CONFIG_ROOT}/backrest:/config
      - ${CONFIG_ROOT}/backrest/data:/data
      - /mnt/usb/server-backup:/mnt/usb/server-backup
      - ${DATA_ROOT}:/data-source:ro
      - ${CONFIG_ROOT}:/config-source:ro
      - /var/tmp/backrest-dumps:/var/tmp/backrest-dumps
    ports:
      - "9898:9898"
    networks:
      - homelab_net
```
</details>

---