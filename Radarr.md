Radarr é um software que gerencia sua coleção de filmes para Usenet e BitTorrent1. Radarr pode monitorar vários feeds RSS para novos filmes e se comunicar com clientes e indexadores para baixar, organizar e renomear eles. Radarr também pode ser configurado para atualizar automaticamente a qualidade dos arquivos existentes na biblioteca quando um formato de melhor qualidade estiver disponível

### Links
**[Docker Hub](https://hub.docker.com/r/linuxserver/radarr)**
**[Radarr](https://radarr.video/)**

---
### Docker Compose

```yaml
---
version: "2.1"
services:
  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/data:/config
      - /path/to/movies:/movies #optional
      - /path/to/downloadclient-downloads:/downloads #optional
    ports:
      - 7878:7878
    restart: unless-stopped
```


