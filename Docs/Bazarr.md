É um aplicativo complementar ao Sonarr e Radarr. Ele gerencia e baixa legendas com base em seus requisitos.

**[Docker Hub](https://hub.docker.com/r/linuxserver/bazarr) [Bazarr](https://www.bazarr.media/)**


```yaml
---
version: "2.1"
services:
  bazarr:
    image: lscr.io/linuxserver/bazarr:latest
    container_name: bazarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/bazarr/config:/config
      - /path/to/movies:/movies #optional
      - /path/to/tv:/tv #optional
    ports:
      - 6767:6767
    restart: unless-stopped
```
