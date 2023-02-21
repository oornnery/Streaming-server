É um Sistema de Mídia de Software Livre que permite controlar o gerenciamento e a transmissão de sua mídia. Ele é uma alternativa aos Emby e Plex proprietários, para fornecer mídia de um servidor dedicado para dispositivos de usuário final por meio de vários aplicativos

**[Docker Hub](https://hub.docker.com/r/linuxserver/jellyfin) [Jellyfin](https://jellyfin.org/)**

```yaml
---
version: "2.1"
services:
  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - JELLYFIN_PublishedServerUrl=192.168.0.5 #optional
    volumes:
      - /path/to/library:/config
      - /path/to/tvseries:/data/tvshows
      - /path/to/movies:/data/movies
    ports:
      - 8096:8096
      - 8920:8920 #optional
      - 7359:7359/udp #optional
      - 1900:1900/udp #optional
    restart: unless-stopped
```
