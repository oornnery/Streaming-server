É um software que gerencia sua coleção de séries de TV para Usenet e BitTorrent4. Sonarr pode monitorar vários feeds RSS para novos episódios e se comunicar com clientes e indexadores para baixar, organizar e renomear eles.

**[Docker Hub](https://hub.docker.com/r/linuxserver/sonarr) [Sonarr](https://sonarr.tv/)**

```yaml
---
version: "2.1"
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/data:/config
      - /path/to/tvseries:/tv #optional
      - /path/to/downloadclient-downloads:/downloads #optional
    ports:
      - 8989:8989
    restart: unless-stopped
```
