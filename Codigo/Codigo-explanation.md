# Codigo

### Fragmento de VPN con WireGuard

```docker
# Este fragmento es de solo la VPN con Wireguard

version: "3.7"
services:
  wireguard:
    image: lscr.io/linuxserver/wireguard:latest
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Mexico_City
      - SERVERURL=wireguard.myhome.com # DNS dinámico
      - SERVERPORT=51820
      - PEERS=4 # 4 clientes
      - PEERDNS=auto # Quad9
      - INTERNAL_SUBNET=10.13.13.0/24 # Red WireGuard
      - LOG_CONFS=true
    volumes:
      - /root/volumes/wireguard:/config
      - /lib/modules:/lib/modules
      - /usr/src:/usr/src
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```

### Fragmento de PI-Hole

```docker
# Este fragmento es de solo del servidor DNS de Pi-hole

version: "3.7"
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp"
      - "80:80/tcp"
      - "443:443/tcp"
    environment:
      TZ: 'America/Mexico_City'
      WEBPASSWORD: 'yourpassword'
    volumes:
      - './etc-pihole/:/etc/pihole/'
      - './etc-dnsmasq.d/:/etc/dnsmasq.d/'
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```

### Combinación

```docker
version: '3.7'

services:
  wireguard:
    image: linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Mexico_City
      - SERVERPORT=51820 #optional
      - PEERS=2 #numero de dispositivos permitidos
      - PEERDNS=auto #optional
      - INTERNAL_SUBNET=10.13.13.0 #optional
    volumes:
      - /root/wireguard:/config
      - /lib/modules:/lib/modules
      - /usr/src:/usr/src
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    dns:
      - 172.20.0.7
    restart: unless-stopped
    networks:
      containers:
        ipv4_address: 172.20.0.6

  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp"
      - "80:80/tcp"
      - "443:443/tcp"
    environment:
      TZ: 'America/Mexico_City'
      WEBPASSWORD: 'yourpassword'
    volumes:
      - './etc-pihole/:/etc/pihole/'
      - './etc-dnsmasq.d/:/etc/dnsmasq.d/'
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
    networks:
      containers:
        ipv4_address: 172.20.0.7

networks:
  containers:
    ipam:
      config:
        - subnet: 172.20.0.0/24

```

[docker-compose.yml](docker/docker-compose.yml)
