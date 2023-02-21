Jellyseerr é um aplicativo de software gratuito e de código aberto para gerenciar solicitações para sua biblioteca de mídia. É um fork do Overseerr criado para trazer suporte para os servidores de mídia Jellyfin e Emby.

**[Docker Hub](https://hub.docker.com/r/fallenbagel/jellyseerr) [GitHub](https://github.com/Fallenbagel/jellyseerr)**


```yaml
version: '3'
services:
    jellyseerr:
       image: fallenbagel/jellyseerr:latest
       container_name: jellyseerr
       environment:
            - LOG_LEVEL=debug
            - TZ=Asia/Tashkent
       ports:
            - 5055:5055
       volumes:
            - /path/to/appdata/config:/app/config
       restart: unless-stopped
```

