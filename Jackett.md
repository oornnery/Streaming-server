
### Documentação e links:

**[GitHub](https://github.com/Jackett/Jackett)**
**[YouTube](https://www.youtube.com/watch?v=illoFzNpdR4&list=PLxatknzLa1fJwerISUiztTEPKMrwSpKKK&index=4)**
**[Docker](https://hub.docker.com/r/linuxserver/jackett)**

---
### Instalação com Docker

#### Docker compose

```yaml
---
version: "2.1"
services:
  jackett:
    image: lscr.io/linuxserver/jackett:latest
    container_name: jackett
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
      - AUTO_UPDATE=true #optional
    volumes:
      - /path/to/data:/config
      - /path/to/blackhole:/downloads
    ports:
      - 9117:9117
    restart: unless-stopped
```
