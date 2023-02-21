
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

- **[[OpenVPN]]** Um software que permite criar uma rede privada virtual.
	**[openvpn](https://openvpn.net/) [Docker Hub](https://hub.docker.com/r/linuxserver/openvpn-as)**

- **[[Qbittorrent]]** um software de código aberto que permite baixar e compartilhar arquivos usando o protocolo BitTorrent (Depende do **[[OpenVPN]]** para realizar os downloads)
	**[GitHub](https://github.com/qbittorrent/qBittorrent) [Docker Hub](https://hub.docker.com/r/linuxserver/qbittorrent)** 

+ **[[Jackett]]** é um software que permitr usar vários rastreadores de torrents com aplicativos que suportam a API ***Tornab*** ou ***Newznab***
	**[GitHub](https://github.com/Jackett/Jackett) [Docker Hub](https://hub.docker.com/r/linuxserver/jackett)**

+ **[[Radarr]]** é um software que gerencia sua coleção de filmes para Usenet e BitTorrent1. Radarr pode monitorar vários feeds RSS para novos filmes e se comunicar com clientes e indexadores para baixar, organizar e renomear ele. (Depende do **[[Jackett]]** para traduzir a consulta e rastrear o torrent)
	**[Docker Hub](https://hub.docker.com/r/linuxserver/radarr) [Radarr](https://radarr.video/)**

+ **[[Sonarr]]** é um software que gerencia sua coleção de séries de TV para Usenet e BitTorrent4. Sonarr pode monitorar vários feeds RSS para novos episódios e se comunicar com clientes e indexadores para baixar, organizar e renomear eles. (Depende do **[[Jackett]]** para traduzir a consulta e rastrear o torrent)
	**[Docker Hub](https://hub.docker.com/r/linuxserver/sonarr) [Sonarr](https://sonarr.tv/)**

+ **[[Bazarr]]** é um aplicativo complementar ao Sonarr e Radarr. Ele gerencia e baixa legendas com base em seus requisitos. (Depende do **[[Jackett]]** para traduzir a consulta e rastrear o torrent)
	**[Docker Hub](https://hub.docker.com/r/linuxserver/bazarr) [Bazarr](https://www.bazarr.media/)**

- **[[Liddar]]** é um método para determinar distâncias ao mirar um objeto ou uma superfície com um laser e medir o tempo para a luz refletida retornar ao receptor
	**[Docker Hub](https://hub.docker.com/r/linuxserver/lidarr) [Lidarr](https://lidarr.audio/)**

- **[[Prowlarr]]**  é um gerenciador/proxy de indexadores que se integra com seus vários aplicativos PVR. Prowlarr suporta o gerenciamento de rastreadores de torrent e indexadores de Usenet12. Ele se integra perfeitamente com Lidarr, Mylar3, Radarr, Readarr e Sonarr oferecendo o gerenciamento completo de seus indexadores sem necessidade de configuração por aplicativo
	**[Docker Hub](https://hub.docker.com/r/linuxserver/prowlarr) [Prowlarr](https://prowlarr.com/)**

- **[[Ombi]]**  Ombi é um aplicativo web auto-hospedado que permite que seus usuários compartilhados do Plex ou Emby solicitem conteúdo por si mesmos.
	**[Docker Hub](https://hub.docker.com/r/linuxserver/ombi) [Ombi](https://ombi.io/)**

- **[[Jellyseerr]]**  é um aplicativo de software gratuito e de código aberto para gerenciar solicitações para sua biblioteca de mídia. É um fork do Overseerr criado para trazer suporte para os servidores de mídia Jellyfin e Emby
	**[Docker Hub](https://hub.docker.com/r/fallenbagel/jellyseerr) [GitHub](https://github.com/Fallenbagel/jellyseerr)**

- **[[Rclone]]** é um programa de linha de comando para gerenciar arquivos em armazenamento na nuvem.
	**[Docker Hub](https://hub.docker.com/r/rclone/rclone) [Rclone](https://rclone.org)**

- **[[Jellyfin]]** é um Sistema de Mídia de Software Livre que permite controlar o gerenciamento e a transmissão de sua mídia. Ele é uma alternativa aos Emby e Plex proprietários, para fornecer mídia de um servidor dedicado para dispositivos de usuário final por meio de vários aplicativos
	**[Docker Hub](https://hub.docker.com/r/linuxserver/jellyfin) [Jellyfin](https://jellyfin.org/)**

- **[[Plex]]** é um sistema de mídia que permite transmitir filmes e programas de TV em quase qualquer dispositivo. Ele também oferece TV ao vivo, notícias e canais gratuitos
	**[Docker Hub](https://hub.docker.com/r/linuxserver/plex) [Plex](https://www.plex.tv/)**



### Criando diretorios.

### Criando arquivo do docker-compose.


### Configuração dos programas;



