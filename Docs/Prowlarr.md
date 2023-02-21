É um gerenciador/proxy de indexadores que se integra com seus vários aplicativos PVR. Prowlarr suporta o gerenciamento de rastreadores de torrent e indexadores de Usenet12. Ele se integra perfeitamente com Lidarr, Mylar3, Radarr, Readarr e Sonarr oferecendo o gerenciamento completo de seus indexadores sem necessidade de configuração por aplicativo

**[Docker Hub](https://hub.docker.com/r/linuxserver/prowlarr) [Prowlarr](https://prowlarr.com/)**

```yaml
---
version: "2.1"
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/data:/config
    ports:
      - 9696:9696
    restart: unless-stopped
```
