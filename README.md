
# Requisitos de hardware

* Linux Server. 
* Memoria RAM 4G.
- CPU 2.
- Memoria sufuciente para armazenar as mídias.

### Preparando o servidor.

Estou usando o Ubuntu-Server:22.04 no **[[Multipass]]**, você pode usar qualquer outro linux server.

Para criar a imagem, use comando abaixo. 

```PowerShell
multipass launch --cpus 2 --memory 4G --disk 60G --name "media-center" 22.04
```

O comando ``multipass launch`` é usado para criar uma nova imagem, você  pode listar novas imagens com o comando ``multipass find`` ou ``multipass --help`` para ver todas as opções. 

Definimos a quantidade de CPU usada com o ``--cpus 2`` , agora para a memoria RAM use ``--memory 2G`` (podemos usar K, M e G) e escolhi 60G de espaço para inicial para isso use ``--disk 60G``, para definir um nome use ``--name "media-center"`` como ultimo parametro a imagem ``22.10`` se você usar o comando ``find`` mencionado acima, vai observar que se refere ao Ubuntu:22.10.

Após concluído você deve ver essa saída.

```PowerShell
>>> multipass launch --cpus 2 --memory 2G --disk 60G --name "media-center" 22.10
Launched: media-center
Skipping mount due to disabled mounts feature
```

Para listar suas imagens, use ``multipass list``:

```PowerShell
>>> multipass list
Name                    State             IPv4             Image
primary                 Suspended         --               Ubuntu 22.04 LTS
docker                  Stopped           --               Ubuntu 22.04 LTS
media-center            Running           172.26.172.184   Ubuntu 22.04 LTS
```


### Acessando servidor.

```PowerShell
PS C:\Users\fabio> multipass shell media-center
```

Uma vez que você acessou o shell da imagem criada, podemos iniciar a instalação e configuração. 

```PowerShell
>>> multipass shell media-center
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-60-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue Feb 21 12:18:35 -03 2023

  System load:  0.0               Processes:             100
  Usage of /:   2.5% of 57.97GB   Users logged in:       0
  Memory usage: 11%               IPv4 address for eth0: 172.26.172.184
  Swap usage:   0%


 * Introducing Expanded Security Maintenance for Applications.
   Receive updates to over 25,000 software packages with your
   Ubuntu Pro subscription. Free for personal use.

     https://ubuntu.com/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@media-center:~$
```


### Atualizando o sistema

Após a instalação vamos atualizar o sistema, use o comando abaixo:

```Shell
ubuntu@media-center:~$ sudo apt-get update
```


### Instalando o Docker

Agora vamos instalar o Docker, podemos instalar direto no Ubuntu, porem acredito que para controle, observabilidade e manutenção, a melhor escolha seja o uso de docker. 

Acesse a documentação do Docker

**Para instalar o Docker, use:**  ``sudo apt-get install docker docker-compose
```Shell
ubuntu@media-center:~$ sudo apt-get install docker docker-compose
```

**Para conferir a instalação, use:** ``docker --version``

```Shell
ubuntu@media-center:~$ docker --version
Docker version 20.10.12, build 20.10.12-0ubuntu4
```

 ----

### Apresentando os programas e suas funcionalidades

- **[OpenVPN](./docs/OpenVPN.md)** Um software que permite criar uma rede privada virtual.
	**[openvpn](https://openvpn.net/) [Docker Hub](https://hub.docker.com/r/linuxserver/openvpn-as)**

- **[Qbittorrent](./docs/Qbittorrent.md)** um software de código aberto que permite baixar e compartilhar arquivos usando o protocolo BitTorrent (Depende do **[[OpenVPN]]** para realizar os downloads)
	**[GitHub](https://github.com/qbittorrent/qBittorrent) [Docker Hub](https://hub.docker.com/r/linuxserver/qbittorrent)** 

+ **[Jackett](./docs/Jackett.md)** é um software que permitr usar vários rastreadores de torrents com aplicativos que suportam a API ***Tornab*** ou ***Newznab***
	**[GitHub](https://github.com/Jackett/Jackett) [Docker Hub](https://hub.docker.com/r/linuxserver/jackett)**

+ **[Radarr](./docs/Radarr.md)** é um software que gerencia sua coleção de filmes para Usenet e BitTorrent1. Radarr pode monitorar vários feeds RSS para novos filmes e se comunicar com clientes e indexadores para baixar, organizar e renomear ele. (Depende do **[[Jackett]]** para traduzir a consulta e rastrear o torrent)
	**[Docker Hub](https://hub.docker.com/r/linuxserver/radarr) [Radarr](https://radarr.video/)**

+ **[Sonarr](./docs/Sonarr.md)** é um software que gerencia sua coleção de séries de TV para Usenet e BitTorrent4. Sonarr pode monitorar vários feeds RSS para novos episódios e se comunicar com clientes e indexadores para baixar, organizar e renomear eles. (Depende do **[[Jackett]]** para traduzir a consulta e rastrear o torrent)
	**[Docker Hub](https://hub.docker.com/r/linuxserver/sonarr) [Sonarr](https://sonarr.tv/)**

+ **[Bazarr](./docs/Bazarr.md)** é um aplicativo complementar ao Sonarr e Radarr. Ele gerencia e baixa legendas com base em seus requisitos. (Depende do **[[Jackett]]** para traduzir a consulta e rastrear o torrent)
	**[Docker Hub](https://hub.docker.com/r/linuxserver/bazarr) [Bazarr](https://www.bazarr.media/)**

- **[Lidarr](./docs/Lidarr.md)** é um método para determinar distâncias ao mirar um objeto ou uma superfície com um laser e medir o tempo para a luz refletida retornar ao receptor
	**[Docker Hub](https://hub.docker.com/r/linuxserver/lidarr) [Lidarr](https://lidarr.audio/)**

- **[Prowlarr](./docs/Prowlarr.md)**  é um gerenciador/proxy de indexadores que se integra com seus vários aplicativos PVR. Prowlarr suporta o gerenciamento de rastreadores de torrent e indexadores de Usenet12. Ele se integra perfeitamente com Lidarr, Mylar3, Radarr, Readarr e Sonarr oferecendo o gerenciamento completo de seus indexadores sem necessidade de configuração por aplicativo
	**[Docker Hub](https://hub.docker.com/r/linuxserver/prowlarr) [Prowlarr](https://prowlarr.com/)**

- **[Ombi](./docs/Ombi.md)**  Ombi é um aplicativo web auto-hospedado que permite que seus usuários compartilhados do Plex ou Emby solicitem conteúdo por si mesmos.
	**[Docker Hub](https://hub.docker.com/r/linuxserver/ombi) [Ombi](https://ombi.io/)**

- **[Jellyseerr](./docs/Jellyseerr.md)**  é um aplicativo de software gratuito e de código aberto para gerenciar solicitações para sua biblioteca de mídia. É um fork do Overseerr criado para trazer suporte para os servidores de mídia Jellyfin e Emby
	**[Docker Hub](https://hub.docker.com/r/fallenbagel/jellyseerr) [GitHub](https://github.com/Fallenbagel/jellyseerr)**

- **[Rclone](./docs/Rclone.md)** é um programa de linha de comando para gerenciar arquivos em armazenamento na nuvem.
	**[Docker Hub](https://hub.docker.com/r/rclone/rclone) [Rclone](https://rclone.org)**

- **[Jellyfin](./docs/Jellyfin.md)** é um Sistema de Mídia de Software Livre que permite controlar o gerenciamento e a transmissão de sua mídia. Ele é uma alternativa aos Emby e Plex proprietários, para fornecer mídia de um servidor dedicado para dispositivos de usuário final por meio de vários aplicativos
	**[Docker Hub](https://hub.docker.com/r/linuxserver/jellyfin) [Jellyfin](https://jellyfin.org/)**

- **[Plex](./docs/Plex.md)** é um sistema de mídia que permite transmitir filmes e programas de TV em quase qualquer dispositivo. Ele também oferece TV ao vivo, notícias e canais gratuitos
	**[Docker Hub](https://hub.docker.com/r/linuxserver/plex) [Plex](https://www.plex.tv/)**



### Criando diretorios.

### Criando arquivo do docker-compose.

```Shell
version: '2'
name: media-server
services:
  # openvpn-as:
  #   image: ghcr.io/linuxserver/openvpn-as
  #   container_name: openvpn-as
  #   cap_add:
  #     - NET_ADMIN
  #   environment:
  #     - PUID=1000
  #     - PGID=1000
  #     - TZ=Europe/London
  #     - INTERFACE=eth0 #optional
  #   volumes:
  #     - <path to data>:/config
  #   ports:
  #     - 943:943
  #     - 9443:9443
  #     - 1194:1194/udp
  #     # qbittorrent ports
  #     - 5080:5080
  #     - 6881:6881
  #     - 6881:6881/udp
  #     # prowlarr ports
  #     - 9696:9696
  #   restart: unless-stopped

  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    # depends_on:
    #   - openvpn-as
    # network_mode: service:openvpn-as # Comment this line if vpn is disabled
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
      - WEBUI_PORT=8080
    volumes:
      - qbittorrent-config:/config
      - torrent-downloads:/downloads
    # Uncomment below ports if VPN is disabled.
    ports:
      - 8080:8080
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped

  jackett:
    image: lscr.io/linuxserver/jackett:latest
    container_name: jackett
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
      - AUTO_UPDATE=true #optional
    volumes:
      - jackett-config:/config
      - jackett-blackhole:/downloads
    ports:
      - 9117:9117
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
    volumes:
      - radarr-config:/config
      - radarr-movies:/movies
      - torrent-downloads:/downloads
    ports:
      - 7878:7878
    restart: unless-stopped

  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
    volumes:
      - sonarr-config:/config
      - sonarr-tvseries:/tv
      - torrent-downloads:/downloads
    ports:
      - 8989:8989
    restart: unless-stopped

  bazarr:
    image: lscr.io/linuxserver/bazarr:latest
    container_name: bazarr
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
    volumes:
      - bazarr-config:/config
      - bazarr-movies:/movies
      - torrent-downloads:/downloads
    ports:
      - 6767:6767
    restart: unless-stopped

  lidarr:
    image: lscr.io/linuxserver/lidarr:latest
    container_name: lidarr
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
    volumes:
      - lidarr-config:/config
      - lidarr-music:/music
      - torrent-downloads:/downloads
    ports:
      - 8686:8686
    restart: unless-stopped

  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    # # Comment this if vpn is disabled
    # depends_on:
    #   - vpn
    # network_mode: service:vpn # Comment this line if vpn is disabled
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
    volumes:
      - prowlarr-config:/config
    # Uncomment below ports if VPN is disabled.
    ports:
      - 9696:9696
    restart: unless-stopped

  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    networks:
      - mynetwork
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Brazil
    volumes:
      - plex-config:/config
      - sonarr-tvseries:/tv
      - radarr-movies:/movies
      - lidarr-music:/music
    ports:
      - 8096:8096
      - 8920:8920 #optional
      - 7359:7359/udp #optional
      - 1900:1900/udp #optional
    restart: unless-stopped

  jellyseerr:
    image: fallenbagel/jellyseerr:latest
    container_name: jellyseerr
    networks:
      - mynetwork
    environment:
        - LOG_LEVEL=debug
        - TZ=Brazil
    ports:
        - 5055:5055
    volumes:
        - jellyfin-config:/app/config
    restart: unless-stopped

volumes:
  qbittorrent-config:
  torrent-downloads:
  jackett-config:
  jackett-blackhole:
  radarr-config:
  radarr-movies:
  sonarr-config:
  sonarr-tvseries:
  bazarr-config:
  bazarr-movies:
  lidarr-config:
  lidarr-music:
  prowlarr-config:
  jellyfin-config:
  ombi-config:
  tx-config:
  tx-watch:

networks:
  mynetwork:
    external: true
```

### Configuração dos programas;



