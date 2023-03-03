# Documentação e links:

**[Docker](https://hub.docker.com/r/linuxserver/qbittorrent)**
**[GitHub](https://github.com/qbittorrent/qBittorrent)**

### Instalação via Docker:

```yaml
---
version: "2.1"
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - WEBUI_PORT=8080
    volumes:
      - /home/ubuntu/docker/qbittorrent/config:/config
      - /home/ubuntu/docker/qbittorrent/downloads:/downloads
    ports:
      - 8080:8080
      - 6881:6881
      - 6881:6881/udp
    restart: always
```

