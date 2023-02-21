É um sistema de mídia que permite transmitir filmes e programas de TV em quase qualquer dispositivo. Ele também oferece TV ao vivo, notícias e canais gratuitos

**[Docker Hub](https://hub.docker.com/r/linuxserver/plex) [Plex](https://www.plex.tv/)**


```yaml
---
version: "2.1"
services:
  plex:
    image: lscr.io/linuxserver/plex:latest
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - VERSION=docker
      - PLEX_CLAIM= #optional
    volumes:
      - /path/to/library:/config
      - /path/to/tvseries:/tv
      - /path/to/movies:/movies
    restart: unless-stopped
```