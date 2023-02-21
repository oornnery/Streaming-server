É um aplicativo web auto-hospedado que permite que seus usuários compartilhados do Plex ou Emby solicitem conteúdo por si mesmos.

**[Docker Hub](https://hub.docker.com/r/linuxserver/ombi) [Ombi](https://ombi.io/)**

```yaml
---
version: "2.1"
services:
  ombi:
    image: lscr.io/linuxserver/ombi:latest
    container_name: ombi
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - BASE_URL=/ombi #optional
    volumes:
      - /path/to/appdata/config:/config
    ports:
      - 3579:3579
    restart: unless-stopped
```

